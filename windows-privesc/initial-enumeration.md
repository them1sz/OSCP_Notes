# Preliminary Recon

### Windows Privileges & Access Controls

**Security Identifiers (SIDs):** Format: `S-R-X-Y` where R=revision(1), X=authority(5=NT Authority), Y=sub-authorities+RID.

```
S-1-0-0                       Nobody
S-1-1-0                       Everybody
S-1-5-11                      Authenticated Users
S-1-5-18                      Local System
S-1-5-domainidentifier-500    Administrator
```

> RID ≥ 1000 → user-created principal (RID 1000 = first local user, etc.)

### System Enumeration

{% tabs %}
{% tab title="CMD" %}
```ps
hostname          # Machine hostname
whoami            # Logged in user
whoami /groups    # Groups that the user is part of 
whoami /priv      # Special privileges (e.g., SeImpersonatePrivilege)
systeminfo        # System information (patches, version..)
ipconfig /all     # List everything 
route print       # Print routes (e.g., to different subnetworks)
netstat -ano      # Active TCP/UDP connections
dir /a            # Hidden directories (.git, AppData etc)
```
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Get-Process                    # Running processes
ls -Force                      # Hidden directories
Get-ChildItem -Force | Format-List -Property Name, Attributes
```
{% endtab %}
{% endtabs %}

### Registry Enumeration

{% tabs %}
{% tab title="PowerShell / CMD" %}
```powershell
# 32-bit installed apps
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

# 64-bit installed apps
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

# WinLogon
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"

```
{% endtab %}

{% tab title="-" %}
```powershell
```
{% endtab %}
{% endtabs %}

### File Searching

```powershell

# Search whole drive for a file
Get-ChildItem -Path C:\ -Recurse -Filter "procname.*" -File -Force -ErrorAction SilentlyContinue | Select-Object FullName

# Search for KeePass databases
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

# Search XAMPP config files
Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue
```

**Runas:** Use when you have credentials for a user not in RDP/WinRM groups but have GUI access (RDP). Works with local or domain accounts.

## PowerShell History & Logging

**In-session history (can be cleared):**

```powershell
Get-History         # view
```

**PSReadLine history (persisted — PowerShell v5+):**

```powershell
(Get-PSReadlineOption).HistorySavePath
type C:\Users\dave\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

**Script Block Logging:** `Event Viewer > Application and Services Logs > Microsoft > Windows > PowerShell > Operational` Search strings: `cred`, `convert` to find password-related activity.

***

