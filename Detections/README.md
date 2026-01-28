# Detection  Documentation

This directory contains Splunk queries developed to detect the attack campaign documented in this repository. Each detection is designed to be scheduled as an alert within Splunk.

## Detection Catalog

| Detection Name | MITRE ATT&CK Technique | SPL File | Purpose | Severity | Triage Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Firewall Bruteforce Success** | T1110.004, TA0001 | [firewall-bruteforce-investigation.spl](/Investigations/firewall-analysis/spl-queries/firewall-bruteforce-investigation.spl) | Detects multiple failed connections followed by a success to SSH/RDP ports. Indicates likely credential compromise. | High | Correlate with Windows/Linux auth logs for the target IP. Check if source IP is in threat intel feed. |
| **Windows RDP Bruteforce** | T1110.001 | [windows-brute-force-investigation.spl](/Investigations/windows-analysis/spl-queries/windows-brute-force-investigation.spl) | Identifies 5+ failed logins (EventID 4625) for a single account within 10 minutes. | Medium | Verify if account has lockout policy enabled. |
| **Windows Admin External Login** | T1078.002 | [windows-privileged-account-investigation.spl](/Investigations/windows-analysis/spl-queries/windows-privileged-account-investigation.spl) | Alerts on successful admin account logins (EventID 4624) from non-internal source IPs. | Critical | Immediate incident. Verify user intent or assume credential theft. |
| **Malicious PowerShell Detection** | T1059.001 | [windows-process-monitoring-investigation.spl](/Investigations/windows-analysis/spl-queries/windows-process-monitoring-investigation.spl) | Finds `powershell.exe` with `-encodedCommand` flag or execution of `PsExec`. | High | Highly indicative of post-exploitation. Scope for lateral movement. |
| **Linux SSH Bruteforce** | T1110.003| [linux-brute-force-investigation.spl](/Investigations/linux-analysis/spl-queries/linux-brute-force-investigation.spl) | Detects clusters of failed SSH login attempts from a single source. | Medium |Identify targeted user. Search for success after failures. |
| **Linux SSH Root Attack** | T1110.003, T1078 | [root-attacks-investigation.spl](/Investigations/linux-analysis/spl-queries/root-attacks-investigation.spl) | Specifically detects brute force attacks against the root account that were successful. | Critical | Root access achieved. Immediate containment required on target host. |



## Deployment Notes
* **Thresholds:** Adjust `failed_attempts >= 5` thresholds based on environment baselines.
* **Scheduling:** Recommended cron schedule is `*/15 * * * *` for brute-force detections.
* **Action:** All alerts are configured to trigger a "Log Event" to the `_internal` index. In production, integrate with a ticketing system platform.



## Operational Note
The triage steps above outline the initial analyst actions for each detection. For the complete incident response lifecycle—including evidence of containment actions, eradication steps, and reporting, refer to the dedicated **[Incident Response Report](https://github.com/yourusername/incident-response-report-repo)** for this attack campaign.
