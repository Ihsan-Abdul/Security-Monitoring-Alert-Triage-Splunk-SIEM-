# Windows Brute-force Investigation

## What triggered this investigation
Multiple failed Windows authentication attempts (Event ID 4625) were observed for the user `john` from a single source IP.

## What I did
- Identified repeated failed logins
- Pivoted on the affected user
- Pivoted on the source IP
- Reviewed privileged activity (Event ID 4672)
- Built a timeline to reconstruct events

## Timeline
[View timeline](./timeline.png)


![Timeline](./timeline.png)

## Privileged Activity Review (Event ID 4672)
Event ID 4672 indicates special privileges were assigned to an account.  
In this case, the privileged login belonged to a known admin account from a different IP and did not correlate with the brute-force activity.

## Conclusion
- Brute-force behavior suspected
- No evidence of privilege escalation
- Activity documented for monitoring
