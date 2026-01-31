# Security Monitoring & Alert Triage with Splunk SIEM

## Overview
This project demonstrates a hands-on detection workflow using Splunk as a SIEM. It documents the creation of searches, the configuration of alerts, and the investigative process of discovering a simulated multi-stage attack across Windows, Linux, and firewall systems. The goal is to showcase practical skills in log analysis, threat hunting, and security operations.

## Key Skills Demonstrated
*   SIEM/Splunk Operations: Building and scheduling correlation searches (SPL), configuring alerts, and creating dashboards.
*   Detection Engineering: Developing rules to identify brute-force attacks, privilege escalation, lateral movement, and port activity.
*   Incident Investigation: Correlating events from multiple data sources (Firewall, Windows Event Logs, Linux auth logs) to understand attack timeline.
*   Threat Intelligence Application: Mapping findings to the MITRE ATT&CK framework.
*   Security Documentation: Creating detections, alerts and actionable playbooks for Security Operations Center use.

## Quick Start
- **For Detection Logic**: Review the query catalog in `Detections/README.md`
- **For Detailed Analysis**: See the investigation reports in `Investigations`
- **For Triage Procedures**: Follow the playbook in `Playbooks/Alert-Triage-Playbook.md`
- **To Reproduce**: Use the sample logs in `Sample-Logs`

## Project Structure & Navigation
Security-Monitoring-Alert-Triage-Splunk-SIEM/
*  README.md
*  Detections -> Detection queries and Alerts built and documented
*  Investigations -> Analysis and Deep Dives 
*  Playbooks -> Alert triage procedures
*  sample-logs -> Simulated log data

*   For Detection Logic: Review the query catalog and rationale in `Detections/README.md`.
*   For Detailed Analysis: See the in-depth reports in the `Investigations` directory.

## Technical Implementation

### Tools & Data Sources
*   SIEM Platform: Splunk (Free License)
*   Log Sources: Simulated logs from:
    *   Network Firewall (Deny/Allow events on ports 22, 3389, 4444)
    *   Windows Servers (Event IDs 4624, 4625, 4688, 4672)
    *   Linux Servers (SSH auth logs)
 
### Sample Data
The anonymized log samples used in this project are available in the `Sample-Logs` directory:
- `windows-logs.csv` - Windows Event Logs (4624, 4625, 4688, 4672)
- `linux_ssh_logs.csv` - Linux SSH authentication logs
- `firewall_logs.csv` - Firewall deny/allow events

### What I Built
1.  Correlation Searches: Developed SPL queries to detect patterns like multiple fails followed by success for brute-force attacks.
2.  Operational Alerts: Configured scheduled searches with threshold-based triggering and log event actions.
3.  Investigative Analysis: Created targeted searches to uncover privilege escalations and lateral movement.
4.  Triage Playbook: Developed actionable procedures for responding to each detection alert.


### Key Learnings & Insights
*   Attack Patterns: Discovered consistent timing, e.g. 10:00 AM daily and IP rotation are very clear indicators of an automated malicious activity.
*   Correlation: Full scale of events cannot be discovered with firwall logs alone, linking them to Windows and Linux authentication events shows the full breach timeline.
*   Detection Evasion: Attackers used non-standard ports such as 4444 and 4445 for SSH, further reinforcing the need for detection rules that focus on behavior and not just port numbers.
*   Structured Output: Using `eval` to assign severity scores and clear alert names dramatically speeds up triage.

---

## How to Reproduce This Lab

### Prerequisites
1.  Splunk Instance: Download and install Splunk Enterprise (Free) or start a trial.
2.  Sample Data: The anonymized log samples used in this project are available in the `Sample-Logs` directory (See Next Steps below to create this).

### Step-by-Step Setup Guide (Conceptual)
1.  Configure Data Inputs: In Splunk, set up dummy inputs for firewall, Windows, and Linux log formats.
2.  Ingest Sample Logs: Use the sample-log files to populate your Splunk instance with the events described in the investigation reports.
3.  Implement Detections: Search the SPL queries from the detections folder into Splunk searches.
4.  Configure Alerts: Set alert actions per the screenshots in the `Detections` folder.
5.  Investigate: Run the provided investigative queries to trace the attack from initial access to lateral movement.

---


## Related Project: Incident Response Report
This detection project is part one of a two-part portfolio series. The investigation documented here is continued in a dedicated Incident Response Report, which details the full forensic timeline, evidence collection, containment actions, and executive summary.

Link to the companion report: Incident Response Report: Analysis of a 5-Day Brute Force Campaign ([Incident-Response-Report-Repo](https://github.com/Ihsan-Abdul/Incident-Response-Triage-Documentation))

---
