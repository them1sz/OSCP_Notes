# SNMP Enumeration

```bash
# Install MIB translations
apt-get install snmp-mibs-downloader

# Query a specific MIB
snmpwalk -c public -v1 192.168.150.151 1.3.6.1.2.1.25.4.2.1.2

# Force ASCII output
snmpwalk -c public -v1 192.168.150.151 1.3.6.1.2.1.25.4.2.1.2 -Oa
```

**Useful MIB OIDs:**

| OID | Description |
|---|---|
| `1.3.6.1.2.1.25.1.6.0` | System Processes |
| `1.3.6.1.2.1.25.4.2.1.2` | Running Programs |
| `1.3.6.1.2.1.25.4.2.1.4` | Processes Path |
| `1.3.6.1.2.1.25.2.3.1.4` | Storage Units |
| `1.3.6.1.2.1.25.6.3.1.2` | Software Name |
| `1.3.6.1.4.1.77.1.2.25` | User Accounts |
| `1.3.6.1.2.1.6.13.1.3` | TCP Local Ports |
