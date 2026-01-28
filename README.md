# Security Monitoring & Alert Triage with Splunk SIEM

## Overview
This project demonstrates a hands-on detection engineering workflow using Splunk as a SIEM. It documents the creation of correlation searches, the configuration of alerts, and the investigative process to uncover a simulated multi-stage attack across Windows, Linux, and firewall systems. The goal is to showcase practical skills in log analysis, threat hunting, and security operations.

## Key Skills Demonstrated
*   SIEM/Splunk Operations: Building and scheduling correlation searches (SPL), configuring alerts, and creating dashboards.
*   Detection Engineering: Developing rules to identify brute-force attacks, privilege escalation, lateral movement, and anomalous port activity.
*   Incident Investigation: Correlating events across multiple data sources (Firewall, Windows Event Logs, Linux auth logs) to reconstruct an attack timeline.
*   Threat Intelligence Application: Mapping findings to the MITRE ATT&CK framework (T1110, T1059.001, T1021.002, etc.).
*   Security Documentation: Producing detection catalogs and actionable playbooks for Security Operations Center (SOC) use.

## Project Structure & Navigation
Security-Monitoring-Alert-Triage-Splunk-SIEM/
*  README.md # Currently Here
*   Detections # The main queries built and documented
         * README.md # Catalog of SPL queries
*  Investigations # Analysis & Deep Dives 
      *  linux-analysis/
      *  windows-analysis/
      *  firewall-analysis/

*   For Detection Logic: Review the query catalog and rationale in `/detections/README.md`.
*   For Detailed Analysis: See the in-depth reports in the `/Investigations/` directory.

## Technical Implementation

### Tools & Data Sources
*   SIEM Platform: Splunk (Free License)
*   Log Sources: Simulated logs from:
    *   Network Firewall (Deny/Allow events on ports 22, 3389, 4444)
    *   Windows Servers (Event IDs 4624, 4625, 4688, 4672)
    *   Linux Servers (SSH auth logs via `/var/log/auth.log` format)

### What I Built
1.  Correlation Searches: Developed SPL queries to detect patterns like "multiple fails followed by success" for brute-force attacks.
2.  Operational Alerts: Configured scheduled searches with threshold-based triggering and log event actions.
3.  Investigative Analysis: Created targeted searches to uncover privilege escalation (`admin` account usage) and lateral movement (`PsExec`).

### Key Learnings & Insights
*   Attack Patterns are Discoverable: Consistent timing (e.g., 10:00 AM daily) and IP rotation are strong indicators of automated, malicious activity.
*   Correlation is Critical: Isolated events in firewall logs only tell part of the story; linking them to Windows/Linux authentication events reveals the full breach chain.
*   Detection Evasion is Common: Attackers used non-standard ports (4444, 4445) for SSH, reinforcing the need for detection rules that focus on behavior, not just port numbers.
*   The Value of Structured Output: Using `eval` to assign severity scores and clear alert names dramatically speeds up triage.

---

## How to Reproduce This Lab

### Prerequisites
1.  Splunk Instance: Download and install Splunk Enterprise (Free) or start a trial.
2.  Sample Data: The anonymized log samples used in this project are available in the `/sample-logs/` directory (See Next Steps below to create this).

### Step-by-Step Setup Guide (Conceptual)
(A fully reproducible guide with automation is a planned enhancement. The current project focuses on the detection logic and analysis.)
1.  Configure Data Inputs: In Splunk, set up dummy inputs for firewall, Windows, and Linux log formats.
2.  Ingest Sample Logs: Use the sample-log files to populate your Splunk instance with the event sequences described in the investigation reports.
3.  Implement Detections: Search the SPL queries from the detections folder into Splunk as new scheduled searches.
4.  Configure Alerts: Set alert actions per the screenshots in the `Detections/` folder.
5.  Investigate: Run the provided investigative queries to trace the attack from initial access to lateral movement.

---


## Related Project: Incident Response Report
This detection project is part one of a two-part portfolio series. The investigation documented here is continued in a dedicated Incident Response Report, which details the full forensic timeline, containment actions, and executive summary.

Link to the companion report: Incident Response Report: Analysis of a 5-Day Brute Force Campaign (https://github.com/yourusername/incident-response-report-repo)

---
