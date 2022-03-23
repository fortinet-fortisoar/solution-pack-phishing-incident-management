# Advanced Phishing Incident Management

Guided Simulation where a series of automation workflows guides your investigation via the Workspace comments. Comments tagged as *Actions* represent the tasks the analyst must do. *Hints* are simply suggestions

[![Solution Pack Video](https://img.youtube.com/vi/eQ0G_Tgr_4M/0.jpg)](https://www.youtube.com/embed/eQ0G_Tgr_4M)

[Solution Pack Video Introduction](https://www.youtube.com/embed/eQ0G_Tgr_4M)

### 1) Prerequisites

**Generic Prerequisites:**
- Incident Response Content Pack: `yum install -y fsr-ir-content-pack.x86_64`
- SLA Connector configured (part of this solution pack)
- File Content Extraction connector (part of this solution pack)
- MITRE ATT&CK Connector configured with scheduled ingestion
- Solution Pack: [alt-enrichment-playbooks](https://github.com/ftnt-cse/solution-pack-alt-enrichment-playbooks) (Optional)

**For Simulation mode (Fake mock data):**
- Make sure your global variable: `Demo_mode` is set to `true` (Playbook editors > Tools > Global Variables)
- FortiSOAR SOC Simulator Connector configured (1.0.9+)
- FortiGuard Connector configured
- VirusTotal Connector configured

**For Live mode (Real data):**
- MS Exchange/SMTP Connectors configured with your MS Exchange parameters (To send notifications and run remediation actions)
- AD Connector configured with your DC parameters (For users enrichment)
- AlienVaultOTX Connector configured (Optional CTI)
- IPstack Connector configured (Optional CTI)
- APIVoid Connector configured (Optional CTI)
- MXToolBox (Optional CTI)
- HybridAnalysis (Optional CTI)

### 2) Configuration:
#### Global Variables:
You need to set the below global variables in the playbook editor (**Automation > playbooks > (open any playbook) > Tools > Global Variables**)
- **Demo_mode:** if set to **true** the playbooks will use mock data instead of getting it via the connectors
- **Default_Email:** used as email sender

### 3) Installation/Deployment:
- Download the repo's zip from this page, click on: **Code > Download ZIP** and save the ZIP file to your workstation
- Open FortiSOAR import wizard located at: **Settings > Import Wizard**. Click on ![Import From File](import_from_file.png)
- Drag and drop the zip file you downloaded and follow the wizard

### 4) Simulation Steps:
#### 4.1) False Positive Alert: **Immediate action required**
- The email is parsed, you will have to set the status to **Investigating** so the acknowledgment SLA will be computed
- Inspect the various parsed email field such as Body and Headers 
- Run Investigation Playbook < Phishing Alert Enrichment and Investigation >
- Notice The Alert Description, the email is tagged <Internal>
- No malicious indicators found
- The alert is closed as a false positive with a closure note: *Alert closed as False Positive, No Malicious component found*

#### 4.2) True Positive Alert: **Fw: Vulnerability Patching Instructions**
- The email is parsed, you will have to set the status to **Investigating** so the acknowledgment SLA will be computed
- Inspect the various parsed email field such as Body and Headers 
- Run Investigation Playbook **Phishing Alert Enrichment and Investigation**
- Open the Playbook logs and follow the execution of the above playbook
- Email Indicators are extracted and rated, notice the several of them with bad reputation
- The executed playbook will escalate the alert automatically due to the malicious indicators. The alert will be closed for the remaining case investigation will be carried out as an incident by a T2 analyst
- Browse to **Correlations > Incidents** and open the newly escalated incident
- As T2 Analyst start the Incident Management by setting the Incident Status to : **In Progress** and its Phase status to : **Confirmation**
- Browse to Indicators Tab and review the malicious Indicators, there are few of them
- Expand the Incident description and notice the email origin, check if any of the targeted users is a high profile one. Users Active Directory details can be found at **Correlations >  Users**
- Open the file Attachment indicator which looks like: **Password_Update_Guide_XXXX.docx** set its reputation based on the file content displayed on its File Preview field
- Notice there no reputation is found for the file (0 day?), so it's risk factor has to be determined manually. Identify the indicator risk, if high set the Reputation to **Malicious**
- If the case is confirmed True Positive browse to Incident module, set the Phase to **Eradication** and use the Execute button to run the remediation Playbook **Phishing Incident Response**
- Notice how the email sender is blocked on the email gateway and the phishing email is deleted from all recipients mailboxes.

> Now to be sure none of the recipients have actually opened the email and got the asset infected we will hunt for threats in FortiSIEM using the extracted indicators. the presence of the extracted indicators (from various events such as NGFW, EDR...etc) indicates the source asset has been infected

- To run threat hunting playbook, select all indicators in the Incident Indicators TAB (use the select all button), then **execute > Hunt Indicators on FortiSIEM** when an indicator is found its TLP turns to **Red**
- Browse to **Correlations > Hunts** and check the Source Data of each hunt which is the definitive proof the source asset has been infected
- Quarantine the Asset in **Correlations > Assets** by running the playbook **Quarantine Infected Assets** from the execute button after selecting the asset

> Even though the infected assets have been quarantined they remain infected. A manual task for recovery is created. Check it in the Tasks TAB

- Once the tasks marked: **Completed** set the phase to **Aftermath** and close the incident by setting the status to **Resolved**. You will have to provide some info:
  - Resolution: *Email Sender blocked on SEG, Malicious email deleted from all Mailboxes, infected Asset quarantined and recovered*
  - Next Steps: *Create a KB entry for future reference*
  - Incident Summary: *4 employees were targeted with a spear phishing attack, one of them detonated the malicious code (dricardo) and got his asset infected. incident response completed*



### 5) Known issues (7.0.2)
- Fix Playbook "08 Case management / >> Incident - Set Phase Dates"
    - Step: Update Incident Phase
    - Field: Eradication Date
    - Current Value: `{% if vars.currentValue == "Eradication and vars.eradicationdate is none" %} {{@Current_Date}}{% else %}{{vars.eradicationdate}}{% endif %}`
    - Correct Value: `{% if vars.currentValue == "Eradication" and vars.eradicationdate is none %} {{@Current_Date}}{% else %}{{vars.eradicationdate}}{% endif %}`
- Fix Playbook: Case management / Alert > [05] Update Ack and Response Due dates (Post Severity Change)
    - Open the step: **Update Reset Resp SLA Condition** and replace its content with:
```(vars.input.records[0].respSlaStatus.itemValue == ("SLAState" | picklist("Awaiting Action", "itemValue")) and 'Closed' not in vars.input.records[0].status.itemValue) or vars.input.records[0].respSlaStatus.itemValue == ("SLAState" | picklist("NA", "itemValue")) and (vars.input.records[0].status.itemValue != vars.sla_time_list.alertResTrackedOn)```