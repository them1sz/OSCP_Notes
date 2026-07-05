# BloodHound

## SharpHound & BloodHound

```powershell
# Collect AD data
powershell -ep bypass
Import-Module .\SharpHound.ps1
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\stephanie\Desktop\ -OutputPrefix "sharphound-results"
```

**Running SharpHound with specific credentials:**

```powershell
Invoke-BloodHound -CollectionMethod All -LdapUserName john -LdapPassword dqsTwTpZPn#nL -Domain beyond.com
```

```bash
# Start neo4j and BloodHound on Kali
sudo neo4j start           # default: neo4j:neo4j → change to trustno1
bloodhound-start           # drag the zip file into BloodHound
```

> Mark every owned object in BloodHound to reveal attack paths. SharpHound results are only as good as the user who ran it — manually verify paths the tool might miss.

### Cypher Queries

Users Enumeration: `MATCH (m:Users) RETURN m`

Machine Enumeration: `MATCH (m:Computer) RETURN m`

Active Sessions: `MATCH p = (c:Computer)-[:HasSession]->(m:User) RETURN p`

