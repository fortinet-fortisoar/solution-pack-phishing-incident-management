| [Home](https://github.com/fortinet-fortisoar/solution-pack-phishing-incident-management/blob/release/1.0.0/README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appears, search for and select **Phishing Incident Management**.
3. Click the **Phishing Incident Management** solution pack card.
4. Click **Install** on the bottom to begin the installation.

## Prerequisites

The **Phishing Incident Management** solution pack depends on the following solution packs that are installed automatically &ndash; if not already installed.

| Solution Pack Name                | Purpose                                                             |
|:----------------------------------|:--------------------------------------------------------------------|
| SOAR Framework                    | Required for Incident Response modules                              |
| SOC Simulator                     | Required for Scenario Module and SOC Simulator connector            |
| MITRE ATT&CK Enrichment Framework | Required for leveraging the MITRE ATT&CK Knowledge Base             |
| File Content Extraction           | Required for the set of playbooks implementing file extraction use case |

# Configuration

For optimal performance of the **Phishing Incident Management** solution pack, you can install and configure the following connectors:
- Threat intelligence connectors to enrich the context of a given indicator
    - To configure and use the VirusTotal connector as a source of threat intelligence, refer to [Configuring Virus Total](https://docs.fortinet.com/document/fortisoar/2.1.0/virustotal/166/virustotal-v2-1-0#Configuration_parameters)
    - To configure and use the Fortinet FortiGuard connector as a source of threat intelligence, refer to [Configuring  Fortinet FortiGuard Threat Intelligence](https://docs.fortinet.com/document/fortisoar/3.0.0/fortinet-fortiguard-threat-intelligence/242/fortinet-fortiguard-threat-intelligence-v3-0-0#Configuration_parameters)
- An email ingestion process to periodically read emails from a designated inbox and convert them into alerts in FortiSOAR
    - To configure and use the Microsoft Exchange connector for email ingestion, refer to [Configuring Exchange Connector](https://docs.fortinet.com/document/fortisoar/3.4.0/exchange/1/exchange-v3-4-0#Configuring_the_connector)
- A user database solution to get users and asset details
    - To configure and use Microsoft's Active Directory connector, refer to [Configuring Microsoft's Active Directory](https://docs.fortinet.com/document/fortisoar/2.2.0/active-directory/154/active-directory-v2-2-0#Configuration_parameters)