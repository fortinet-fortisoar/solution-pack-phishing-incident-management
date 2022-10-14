| [Home](https://github.com/fortinet-fortisoar/solution-pack-phishing-incident-management/blob/release/1.0.0/README.md) |
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

| Playbook Name                                             | Description                                                                                |
|:----------------------------------------------------------|:-------------------------------------------------------------------------------------------|
| 1 - Create False Positive Alert                           | Create False Positive Phishing Email                                                       |
| 2 - Create True Positive Phishing Email                   | Create scenario alert from a JSON alert record                                             |
| 3 - Create True Positive Phishing Email - Fully Automated | Create scenario alert from a JSON alert record                                             |
| A - Phishing Alert Enrichment and Investigation           | Phishing alert parsing and triage                                                          |
| B - Phishing Incident Response                            | Tracks affected mailboxes and neutralizes the malicious content                            |
| C - Hunt Indicators on FortiSIEM                          | Hunt indicator value on FortiSIEM for the past X Minutes                                   |
| D - Quarantine Infected Assets                            | Block Infected Assets on FortiGate                                                         |
| E - Generate Demo Records                                 | Creates records to populate dashboards and reports                                         |
| > Add Malicious Attachment Comment                        | Adds a helpful guiding comment if the attachment is found to be malicious                  |
| > Add No Reputation Indicators Comment                    | Adds a helpful guiding comment if the attachment's reputation is not available or is blank |
| > Add Status Comments                                     | Adds helpful guiding comments as per the investigation status                              |
| > Extract File Content                                    | Extract File Content and Metadata                                                          |
| > Hunt Indicators on FortiSIEM                            | Hunt indicator value on FortiSIEM for the past X Minutes                                   |
| > Phishing Alert Enrichment and Investigation             | Referenced playbook used to automate **Phishing Alert Enrichment and Investigation**       |
| > Phishing Incident Management - Fully Automated          | Manage incidents in a fully automated manner                                               |
| > Phishing Incident Response                              | Tracks affected mailboxes and neutralizes the malicious content                            |
| > Quarantine Infected Asset                               | Block Infected Asset on FortiGate                                                          |
| > Create or Link Recipient User                           | Creates or link alert related users                                                        |
| > Escalate Alert to Incident                              | Copy alert content to incident                                                             |
| > Track and Delete Phishing Emails                        | Delete malicious content from Mailboxes                                                    |
| > User Enrichment via Active Directory                    | Fetches user data from AD                                                                  |