# Initial Enumeration

## Accessing Systems

**Evil-WinRM (port 5985/5986):**
Requires membership in **Remote Management Users** or **Administrators**.

**RDP (port 3389):**
Requires membership in **Remote Desktop Users** or **Administrators**.
Also requires `SeRemoteInteractiveLogonRight` not be explicitly denied.

---

## Windows Privileges & Access Controls

**Security Identifiers (SIDs):**
Format: `S-R-X-Y` where R=revision(1), X=authority(5=NT Authority), Y=sub-authorities+RID.

```
S-1-0-0                       Nobody
S-1-1-0                       Everybody
S-1-5-11                      Authenticated Users
S-1-5-18                      Local System
S-1-5-domainidentifier-500    Administrator
```
> RID ≥ 1000 → user-created principal (RID 1000 = first local user, etc.)

**Mandatory Integrity Control (MIC) levels:**
| Level | Scope |
|---|---|
| System | Highly trusted user-mode system processes (Winlogon, LSASS) |
| High | Elevated/admin processes |
| Medium | Standard user processes (default) |
| Low | Sandboxed processes (browsers) |
| Untrusted | Highly restricted sources |

**UAC:** Even Administrators run at Medium integrity by default. Processes must explicitly elevate to High to modify system files or sensitive registry keys.

---

## System Enumeration Commands

```powershell
hostname                          # infer machine role (WEB01, MSSQL01...)
whoami /groups                    # current user's groups
net user / Get-LocalUser          # all local users
net localgroup / Get-LocalGroup   # local groups
Get-LocalGroupMember <group>      # members of specific group
systeminfo                        # OS version, architecture
ipconfig /all                     # all network interfaces
route print                       # routing table (discover other subnets)
netstat -ano                      # active TCP/UDP connections with PIDs
Get-Process                       # running processes

# 32-bit installed apps
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname
# 64-bit installed apps
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

# Search whole drive for a file
Get-ChildItem -Path C:\ -Recurse -Filter "procname.*" -File -Force -ErrorAction SilentlyContinue | Select-Object FullName
```

---

## File Enumeration & Runas

```powershell
# Search for KeePass databases
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

# Search XAMPP config files
Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue
```

**Runas:** Use when you have credentials for a user not in RDP/WinRM groups but have GUI access (RDP). Works with local or domain accounts.

---

## PowerShell History & Logging

**In-session history (can be cleared):**
```powershell
Get-History         # view
Clear-History       # delete
```

**PSReadLine history (persisted — PowerShell v5+):**
```powershell
(Get-PSReadlineOption).HistorySavePath
type C:\Users\dave\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

**Script Block Logging:**
`Event Viewer > Application and Services Logs > Microsoft > Windows > PowerShell > Operational`
Search strings: `cred`, `convert` to find password-related activity.

---

## Recon Automation

```powershell
# winPEAS
iwr -uri https://github.com/peass-ng/PEASS-ng/releases/download/20260417-9e62276b/winPEASx64.exe

# Seatbelt (precompiled)
# https://github.com/kraloveckey/ghostpack-binaries/tree/main/Seatbelt
```
