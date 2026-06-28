# Scheduled Tasks

**Key questions for privilege escalation:**
1. Which user account runs the task?
2. What triggers the task?
3. What actions/binaries does the task execute?

**Enumerate scheduled tasks:**
```cmd
schtasks /query /fo LIST /v
```
```powershell
Get-ScheduledTask
```

If the task runs as SYSTEM/admin and you can replace its binary/script, you can escalate privileges.
