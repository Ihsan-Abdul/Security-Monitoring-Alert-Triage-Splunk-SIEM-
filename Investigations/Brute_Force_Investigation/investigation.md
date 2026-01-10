# Windows Brute-force Investigation

## Summary
I investigated multiple failed Windows login attempts (Event ID 4625) for user `john`.  
A successful login followed from the same IP, which could indicate credential compromise.

## Timeline
I created a timeline of all authentication events sorted by time.  
Refer to ![timeline](timeline.png) for details.

## Privileged Activity (Event ID 4672)
Event 4672 shows special privileges were assigned to an admin account.  
This account and IP were different from the brute-force activity.  
No evidence links it to the attempted attack.

## Assessment
- Suspected brute-force attack detected
- No confirmed privilege escalation
