# Capstone Lab Notes

**GenericAll on a user → change their password:**
```cmd
net user robert Password123 /domain
```

**Enumerate all shares across domain:**
```bash
nxc smb 192.168.242.0/24 -u stephanie -p 'LegmanTeamBenzoin!!' --shares
```

**Check for RDP access across subnet:**
```bash
nxc rdp 192.168.163.0/24 -u mike -p 'Darkness1099!' -d corp.com
```
