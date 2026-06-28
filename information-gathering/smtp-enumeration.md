# SMTP Enumeration

SMTP's `VRFY` verifies users; `EXPN` expands mailing lists — both can reveal valid usernames.

```bash
nc -nv 192.168.50.8 25
VRFY root
VRFY idontexist
```
