| [Home](https://github.com/fortinet-fortisoar/solution-pack-phishing-incident-management/blob/release/1.0.0/README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appears, search for and select **Phishing Incident Management**.
3. Click the **Phishing Incident Management** solution pack card.
4. Click **Install** on the bottom to begin the installation.

## Operation Modes
The Solution Pack operates either in:

- **Simulation Mode:** This mode allows you to run the case management process without configuring FortiSOAR integrations with the different systems the use case involves such as Email server, Cyber Threat Intelligence services ...etx. The workflows will generate fake data to populate the records, this is suitable for demo sessions or trainings. To turn demo mode on, you simply need to set the global variable `Demo_mode` to `true`
- **Live Mode:** If you want to use the solution pack to handle your production phishing emails, the above global variable has to be set to `false`. Furthermore some prerequisites are required, the list is available under Prerequisites section of this document

## Prerequisites

The **Phishing Incident Management** solution pack depends on the following solution packs that are installed automatically &ndash; if not already installed.

| Solution Pack Name                | Purpose                                                             |
|:----------------------------------|:--------------------------------------------------------------------|
| SOAR Framework                    | Required for Incident Response modules                              |
| SOC Simulator                     | Required for Scenario Module and SOC Simulator connector            |
| MITRE ATT&CK Enrichment Framework | Required for leveraging the MITRE ATT&CK Knowledge Base             |
| File Content Extraction           | Required for the set of playbooks implementing file extraction use case |

### Prerequisites for Live Mode
- MS Exchange/SMTP Connectors configured with your MS Exchange parameters (To send notifications and run remediation actions)
- AD Connector configured with your DC parameters (For users enrichment)
- Cyber Threat Intelligence integrations for all types of indicators used in the use case. Indicators must be rated automatically either by the built-in Enrichment playbooks or any custom ones you might be using
- Configured integration with FortiSIEM, FortiMail, FortiGate (For Threat Hunting and Incident Response)
- Default Email Sender has to be set (So users would know from where the notifications origin)

# Configuration

For optimal performance of the **Phishing Incident Management** solution pack, you can install and configure the following connectors:
- Threat intelligence connectors to enrich the context of a given indicator
    - To configure and use the VirusTotal connector as a source of threat intelligence, refer to [Configuring Virus Total](https://docs.fortinet.com/document/fortisoar/2.1.0/virustotal/166/virustotal-v2-1-0#Configuration_parameters)
    - To configure and use the Fortinet FortiGuard connector as a source of threat intelligence, refer to [Configuring  Fortinet FortiGuard Threat Intelligence](https://docs.fortinet.com/document/fortisoar/3.0.0/fortinet-fortiguard-threat-intelligence/242/fortinet-fortiguard-threat-intelligence-v3-0-0#Configuration_parameters)
- An email ingestion process to periodically read emails from a designated inbox and convert them into alerts in FortiSOAR
    - To configure and use the Microsoft Exchange connector for email ingestion, refer to [Configuring Exchange Connector](https://docs.fortinet.com/document/fortisoar/3.4.0/exchange/1/exchange-v3-4-0#Configuring_the_connector)
- A user database solution to get users and asset details
    - To configure and use Microsoft's Active Directory connector, refer to [Configuring Microsoft's Active Directory](https://docs.fortinet.com/document/fortisoar/2.2.0/active-directory/154/active-directory-v2-2-0#Configuration_parameters)