# Preliminary Recon

### net.exe

```cmd
net user /domain                        # all domain users
net user <user> /domain                 # specific user details
net group /domain                       # all domain groups
net group "Sales Department" /domain    # users in a specific group
net accounts                            # account/password policy
```

**Check if machine is domain-joined:**

```powershell
(Get-WmiObject Win32_ComputerSystem).PartOfDomain
```

***

## .NET — Find PDC

```powershell
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

# Script to get LDAP path
$PDC = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().PdcRoleOwner.Name
$DN = ([adsi]'').distinguishedName
$LDAP = "LDAP://$PDC/$DN"
$LDAP
```

***

## PowerView

```powershell
# Load (bypass execution policy first)
powershell -ep bypass
Import-Module .\PowerView.ps1

Get-NetDomain                                          # domain info
Get-NetUser | Select cn                               # all usernames
Get-NetUser | select cn,pwdlastset,lastlogon          # check dormant accounts
Get-NetGroup | select cn                              # groups
Get-NetGroup "Sales Department" | select member       # group members
Get-NetComputer | Select operatingsystem,dnshostname  # computers

# Find where current user has local admin access
Find-LocalAdminAccess

# Logged-on sessions (works pre-Win10 build 1709)
Get-NetSession -ComputerName files04 -Verbose
# Newer machines:
.\PsLoggedon.exe \\files04

# SPNs — map services without port scanning
Get-NetUser -SPN | select samaccountname,serviceprincipalname
setspn -L iis_service

# ACL enumeration
Get-ObjectAcl -Identity "Management Department" | ? {$_.ActiveDirectoryRights -eq "GenericAll"} | select SecurityIdentifier,ActiveDirectoryRights
Convert-SidToName <SID>
Find-InterestingDomainAcl -ResolveGUIDs | Where-Object {$_.IdentityReferenceName -match <username>}

# Domain shares
Find-DomainShare
Find-DomainShare -CheckShareAccess    # only shares accessible to current user
```

**Key ACE permissions:**

| Permission               | Effect                                 |
| ------------------------ | -------------------------------------- |
| `GenericAll`             | Full control over the object           |
| `GenericWrite`           | Edit certain attributes                |
| `WriteOwner`             | Change object ownership                |
| `WriteDACL`              | Edit ACEs on the object                |
| `AllExtendedRights`      | Change/reset passwords                 |
| `ForceChangePassword`    | Reset password without knowing current |
| `Self (Self-Membership)` | Add ourselves to a group               |

***

## SYSVOL — GPP Passwords

SYSVOL share is available to all domain users:

```cmd
ls \\dc1.corp.com\sysvol\corp.com\
```

May contain GPP (Group Policy Preferences) encrypted passwords. Decrypt with:

```bash
gpp-decrypt <cpassword-value>
```



