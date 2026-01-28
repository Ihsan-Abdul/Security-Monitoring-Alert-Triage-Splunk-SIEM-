# Detection  Documentation

This directory contains Splunk queries developed to detect the multi-stage attack campaign documented in this repository. Each detection is designed to be scheduled as an alert within a SIEM.

## Detection Catalog

| Detection Name | MITRE ATT&CK Technique | SPL File | Purpose | Severity | Expected FP Rate | Triage Notes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Firewall Bruteforce Success** | T1110.004, TA0001 | [firewall-bruteforce-investigation.spl](/Investigations/firewall-analysis/spl-queries/firewall-bruteforce-investigation.spl) | Detects multiple failed connections followed by a success to SSH/RDP ports. Indicates likely credential compromise. | High | Low | 1. Correlate with Windows/Linux auth logs for the target IP. 2. Check if source IP is in threat intel feed. |
| **Windows RDP Bruteforce** | T1110.001 | [windows-brute-force-investigation.spl](/Investigations/windows-analysis/spl-queries/windows-brute-force-investigation.spl) | Identifies 5+ failed logins (EventID 4625) for a single account within 10 minutes. | Medium | Medium | Common for service accounts. Verify if account has lockout policy enabled. |





| **Windows Admin External Login** | T1078.002 | [windows-privileged-account-detection.spl](windows-privileged-account-detection.spl) | Alerts on successful admin account logins (EventID 4624) from non-RFC1918 source IPs. | Critical | Low | Immediate incident. Verify user intent or assume credential theft. |
| **Malicious PowerShell Detection** | T1059.001 | [windows-process-monitoring-detection.spl](windows-process-monitoring-detection.spl) | Finds `powershell.exe` with `-encodedCommand` flag or execution of `PsExec`. | High | Low | Highly indicative of post-exploitation. Scope for lateral movement. |
| **Linux SSH Root Bruteforce** | T1110.003 | [linux-root-attacks-detection.spl](linux-root-attacks-detection.spl) | Detects failed root SSH attempts followed by success, including on non-standard ports. | Critical | Low | Root access achieved. Immediate containment required on target host. |

## Deployment Notes
* **Thresholds:** Adjust `failed_attempts >= 5` thresholds based on environment baselines.
* **Scheduling:** Recommended cron schedule is `*/10 * * * *` for brute-force detections.
* **Action:** All alerts are configured to trigger a "Log Event" to the `_internal` index. In production, integrate with a ticketing system (e.g., ServiceNow) or SOAR platform.
