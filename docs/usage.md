| [Home](https://github.com/fortinet-fortisoar/solution-pack-phishing-incident-management/blob/release/1.0.0/README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Usage

Refer to [Simulate Scenario documentation](https://github.com/fortinet-fortisoar/solution-pack-soc-simulator/blob/develop/docs/usage.md) to understand how to simulate and reset scenarios.

To understand the process FortiSOAR follows to manage phishing incidents, we have included a scenario &mdash; **Advanced Phishing Incident Management** with this solution pack. Refer to the section *Advanced Phishing Incident Management* to understand how this solution pack's automation addresses your needs.

## Advanced Phishing Incident Management

This scenario generates an example alert of **Type** *Suspicious Email* in FortiSOAR's Alerts module.

### False Positive Alert

This section helps create a false positive alert to understand how this solution pack's automation addresses your needs.

1. Browse to **Alerts**.
2. Click **Execute** > **1 - Create False Positive Alert**.
3. Inspect the various parsed email fields such as
    - From
    - Subject
    - Body
    - Headers
4. Select the Alert.
5. Click **Execute** > **Phishing Alert Enrichment and Investigation**.
6. Observe the following:
    - The email is tagged *Internal* under **Alert Description**
    - No malicious indicators were found
    - The alert is closed as a false positive with a closure note:
      > *Alert closed as False Positive, No Malicious component found*

### True Positive Alert

This section helps create a true positive alert to understand how this solution pack's automation addresses your needs.

1. Browse to **Alerts**.
2. Click **Execute** > **2 - Create True Positive Phishing Email**.
3. Inspect the various parsed email fields such as
    - From
    - Subject
    - Body
    - Headers
4. Select the Alert.
5. Click **Execute** > **Phishing Alert Enrichment and Investigation**.
6. Observe the following:
    - Email Indicators are extracted and rated
    - Presence of malicious indicators ensures automatic escalation of alerts
    - Depending on the user's role, the alert is either escalated to an incident or marked as resolved and closed

> **NOTE**: The malicious indicators are fetched from a Cyber Threat Intelligence(CTI) platform and hence sometimes all indicators turn out to be false positives. You may need to repeat the steps until you get at least one malicious indicator.

#### Escalated to Incident

In case the alert is escalated, it appears as an incident for the next-level SOC analyst.

1. Open the newly escalated incident.
2. As a next-tier analyst start the Incident Management by setting the incident status to **In Progress** and its phase status to **Confirmation**.
3. Browse to the **Indicators** tab and review the malicious indicators.
4. Users' Active Directory details can be found at **Correlations >  Users**.
5. Open the file Attachment indicator and set its reputation based on the file content displayed in the **File Preview**.
6. Identify the indicator risk and set the Reputation to **Malicious**, if required.
7. Set the Phase to **Eradication** and use the **Execute** button to run the remediation Playbook **Phishing Incident Response**.
    - Notice how the email sender is blocked on the email gateway and the phishing email is deleted from all recipients mailboxes.

### Threat Hunting

To be sure that none of the recipients have opened the email and got the asset infected we hunt for threats in FortiSIEM using the extracted indicators. The presence of the extracted indicators indicates the source asset has been infected.

1. Select all the indicators in the **Incident Indicators** tab
2. Click **Execute > Hunt Indicators on FortiSIEM**. When an indicator is found its Traffic Light Protocol(TLP) turns to **Red**.
3. Browse to **Correlations > Hunts** and check the Source Data of each hunt to determine if the source asset is infected.
4. Click **Execute > Quarantine Infected Assets** to quarantine the asset.
    >**NOTE**: Even though the infected assets have been quarantined they remain infected. The **Tasks** tab lists a manual task for recovery.
5. After the completion of the task, set the phase to **Aftermath**.
6. Set the status to **Resolved** to close the incident. Enter the following information:
    - Resolution
    - Next Steps
    - Incident Summary
7. Click **Generate Incident Summary Report**.

### Fully Automated Case Management with True Positive Alert

Select **3 - Create True Positive Phishing Email - Fully Automated** to create an alert. This Alert is a demonstration of how alert case management can be fully automated.
- Open the alert, and check the playbook logs to track all the executed ones
- Open the escalated record and check all the executed playbooks for the incident, indicators, and assets
- Notice all-time metrics to see how long the automated process took

### Dashboard

The following helps you experience the Dashboard interface.

1. Navigate to **Automation > Playbooks > 12 - Solution Pack Advanced Phishing**.
2. Run the playbook **E - Generate Demo Records** to populate the system with demo records useful for this step.
3. Browse to **Dashboard** and select **Phishing Case Management**.