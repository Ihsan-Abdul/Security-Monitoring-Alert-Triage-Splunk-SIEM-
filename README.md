# Security-Monitoring-Alert-Triage-Splunk-SIEM-

## Overview
This project documents my analysis of firewall, Windows, and Linux logs to identify and investigate a multi-stage security attack. Over the course of this investigation, I discovered a coordinated attacks targeting critical systems across the environment.

## What Happened
Attackers executed a 5-day campaign against the network with daily precision:
- **Morning attacks**: Targeted Linux SSH servers (10:00 AM daily)
- **Afternoon attacks**: Targeted Windows RDP servers (3:00 PM daily)  
- **Post-compromise activity**: Privilege escalation and lateral movement attempts
- **Consistent success**: Attackers gained access every single day

## Key Findings:

### Firewall Attacks
- Brute force attacks against SSH (port 22) and RDP (port 3389)
- 100% success rate - attackers got in every time
- Daily pattern at 10:00 AM and 3:00 PM
- Multiple source IPs rotating: 203.0.113.88, 203.0.113.45, 198.51.100.77

[See detailed firewall analysis](firewall-analysis/firewall-attacks.md)

### Windows Attacks  
- Daily compromise of 'john' account via brute force
- Privilege escalation to 'admin' account
- Malicious PowerShell execution with encoded commands
- Lateral movement attempts using PsExec to domain controller

[See detailed Windows analysis](windows-analysis/windows-attacks.md)

### Linux Attacks
- Root account compromise via SSH brute force
- Attackers used non-standard ports (4444, 4445) to evade detection
- Same attack infrastructure as Windows attacks
- Full system control achieved daily

[See detailed Linux analysis](linux-analysis/linux-attacks.md)

## What I Built
For this investigation, I created several Splunk detection queries:

### Detection Queries Developed:
1. **Brute Force Detection** - Identifies multiple failed attempts followed by success
2. **Privileged Account Monitoring** - Flags admin accounts accessed from external IPs
3. **Malicious Process Detection** - Finds encoded PowerShell and lateral movement tools
4. **Non-Standard Port Detection** - Identifies services running on unusual ports

## What I Learned:

### Technical Insights:
1. **Attackers follow patterns** - The same timing daily made detection easier once I knew what to look for
2. **Cross-platform targeting is common** - Attackers went after both Windows AND Linux, not one or the other
3. **Port changes don't hide attacks** - Using ports 4444/4445 instead of 22 didn't prevent detection
4. **Post-compromise activity tells the story** - The initial breach was just the beginning

### Investigation Takeaways:
- **Correlation is key** - Looking at firewall, Windows, and Linux logs together revealed the full attack chain
- **Timing matters** - Consistent attack times (10 AM, 3 PM) indicated automation
- **IP rotation is a red flag** - Different source IPs each day suggested coordinated infrastructure
- **Success breeds repetition** - Since they succeeded day 1, they kept coming back

### Splunk Skills Developed:
- Writing effective stats queries with time windows
- Using eval for conditional logic and severity scoring
- Creating actionable alerts from detection logic
- Structuring searches for both detection and investigation phases

### Security Mindset Shift:
1. **Initial access patterns** (how they get in)
2. **Privilege escalation** (how they get more access)  
3. **Lateral movement** (how they spread)
4. **Command and control** (how they communicate out)
5. **Data exfiltration** (what they steal)

## Files in This Repository

### Documentation:
- `README.md` - This overview file
- `firewall-analysis/firewall-attacks.md` - Firewall attack analysis
- `windows-analysis/windows-attacks.md` - Windows attack analysis  
- `linux-analysis/linux-attacks.md` - Linux attack analysis

### Detection Queries:
- 9 Splunk query files (.spl) across three categories
- Each query designed to detect specific attack patterns

### Evidence:
- 10 screenshot files (.png) showing actual detection results
- Visual proof of the attacks found

---

*This project demonstrates practical security monitoring skills using Splunk to detect and investigate real-world attack patterns.*
