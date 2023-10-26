| [Home](../README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Contents

## Connectors

| Name                                    | Description                                                                                                                                                                           |
|:----------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fortinet FortiGuard Threat Intelligence | It provides threat intelligence to protect them from malicious cyber attacks.                                                                                                         |
| VirusTotal                              | This connector facilitates automated operations such as scanning and analyzing suspicious files and URLs and retrieving reports from VirusTotal for files, IP addresses, and domains. |

## Module Schemas

| Name       | Description                                                                                               |
|:-----------|:----------------------------------------------------------------------------------------------------------|
| Indicators | **Indicators of compromise** (IOCs) serve as evidence of probable intrusions on a host system or network. |
| Users      | Schema containing user details like email address, manager's name, assets, and domains                    |
| Scenario   | A schema for listing scenarios included with other solution packs that are installed.                     |

## Global Variables

| Name                  | Description                                                                                   |
|:----------------------|:----------------------------------------------------------------------------------------------|
| `Excludelist_IPs`     | Contains a list of IP addresses excluded from the indicator extraction process                |
| `Excludelist_URLs`    | Contains a list of URLs excluded from the indicator extraction process                        |
| `Excludelist_Domains` | Contains a list of domain names excluded from the indicator extraction process                |
| `Demo_mode`           | Enables playbook to execute a mock output                                                     |
| `Excludelist_Hosts`   | Contains a list of host names excluded from the indicator extraction process                  |
| `Hint_Icon`           | Contains style elements required to render a Hint icon within the **Comment** section         |
| `Action_Icon`         | Contains style elements required to render an action icon within the **Comment** section      |
| `Exclamation_Icon`    | Contains style elements required to render an exclamation icon within the **Comment** section |
| `Current_Date`        | Contains the current date                                                                     |
| `Tomorrow_Date`       | Contains the next day's date                                                                  |

## Record Set

| Name     | Description                           |
|:---------|:--------------------------------------|
| Scenario | Advanced Phishing Incident Management |

## Playbook Collection

| 02 - Use Case - Phishing Incident Management |
|:---------------------------------------------|

| Playbook Name                                               | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- |
| 01 - Phishing Alert- Enrichment and Investigation            | Phishing alert parsing and triage                          |
| 02 - Phishing Incident Management - Investigation and Response | Tracks affected mailboxes and neutralizes the malicious content |
| 03 - Phishing Incident Management - Phishing Incident Response via Approval | Implement Remediation Actions subject to SOC Approval (Requires Working Emails) |
| 04 - Hunt Indicators (FortiSIEM)                          | Hunt indicator value on FortiSIEM for the past X Minutes   |
| 05 - Quarantine Infected Assets                            | Block Infected Assets on FortiGate                         |
| A - Scenario - Phishing Incident Management - Create Phishing Demo Records | Creates records to populate dashboards and reports         |
| Add Malicious Attachment Comment to Incident and Indicator | Add malicious attachment comment to an indicator and an incident |
| B - Scenario - Phishing Incident Management - Create True Positive Phishing Email | Create scenario alert from a JSON alert record            |
| C - Scenario - Phishing Incident Management - Create False Positive Alert | Create False Positive Phishing Email                   |
| D - Scenario - Phishing Incident Management - Create True Positive Phishing Email - Fully Automated | Create scenario alert from a JSON alert record |
| Extract File Content and Metadata                           | Extract File Content and Metadata                          |
| Indicators - Add No Reputation Comment                       | Add comment No reputation found, and analyst has to be determined manually. Identify the indicator risk, if high set the Reputation to Malicious |
| Phishing Alert - Add Status Comments                       | Add status comments to alert                                |
| Phishing Alert - Auto Enrichment                            | Extra Attributes Parsers and Alert Triage                    |
| Phishing Alert - Create or Link Recipient User              | Creates or links alert-related users                         |
| Phishing Alert - Escalate Alert to Incident                 | Malicious or Suspicious indicator found, hence escalate phishing alert to incident |
| Phishing Alert - Get Related Indicators Reputations         | Retrieves Reputation values and status for each indicator related to the input Alert |
| Phishing Incident Management - Hunt Indicators (FortiSIEM)  | Hunt indicator value on FortiSIEM for the past X Minutes    |
| Phishing Incident Management - Incident Response            | Tracks affected mailboxes and neutralizes the malicious content |
| Phishing Incident Management - Manage Incident (Fully Automated) | Manage the incident in a fully automated manner            |
| Phishing Incident Management - Quarantine Infected Asset (FortiGate) | Block Infected Asset on FortiGate                  |
| Phishing Incident Management - Track and Delete Phishing Emails | Delete malicious content from Mailboxes                   |
| User Enrichment - Active Directory                         | Fetches user data from AD                                  |
