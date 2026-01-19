# Firewall Attack Analysis

## Overview
Analysis of firewall logs revealed a 5-day brute force campaign targeting SSH and RDP ports. Attackers gained access every day using coordinated attacks at consistent times.

## What Happened
- **Morning attacks (10:00 AM)**: SSH brute force on port 22
- **Afternoon attacks (3:00 PM)**: RDP brute force on port 3389  
- **Pattern**: 6-8 failed attempts followed by successful access
- **Duration**: January 8-12, 2024 (5 consecutive days)

## Key Findings

### Compromised Systems
- **Linux Server (192.168.1.100)**: SSH access via port 4444
- **Windows Server (192.168.1.21)**: RDP access via port 3389

### Attacker Infrastructure
Three rotating source IPs:
- **203.0.113.88**: January 8 & 12
- **203.0.113.45**: January 9 & 10  
- **198.51.100.77**: January 11

### Attack Characteristics
- **100% success rate**: Every attack resulted in access
- **Time consistency**: Same attack windows daily
- **Port targeting**: Focused on management ports (22, 3389)
- **Persistence**: Returned daily despite successful access

![Firewall brute force detection results](screenshots/firewall-bruteforce-detection.png)

## Detection Methodology
Built a Splunk query to identify multiple failed connection and then successful access within 10-minute windows.

[View detection query](spl-queries/firewall-bruteforce-detection.spl)

## MITRE ATT&CK Mapping
- **T1110 - Brute Force**: Password guessing against SSH and RDP
- **T1133 - External Remote Services**: Abuse of internet-facing services
- **TA0001 - Initial Access**: Gaining initial network foothold

## Mitigation Steps
1. **Block attacking IPs** at the firewall immediately
2. **Reset credentials** on all exposed SSH and RDP servers
3. **Account lockout policies** after 3 failed attempts
4. **Reduce attack surface** by limiting internet-facing management services
5. **Enable multi-factor authentication** for remote access

## Connection to Other Attacks
The firewall breaches provided initial access that led to Windows credential compromise and Linux root access.
