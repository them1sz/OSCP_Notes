# SUID, SGID & Capabilities

**Find SUID binaries:**
```bash
find / -perm -u=s -type f 2>/dev/null
find / -perm -4000 2>/dev/null
```

**Find SGID binaries/directories:**
```bash
find / -perm -2000 2>/dev/null
```

**Enumerate capabilities:**
```bash
/usr/sbin/getcap -r / 2>/dev/null
```

> Use [GTFOBins](https://gtfobins.github.io) for exploitation of misconfigured SUID/capability binaries.

> If GTFOBins exploit throws access denied, check `/var/log/syslog` to identify what failed.

**Classic SUID exploit — pkexec (version 0.105):**
Exploit: https://packetstorm.news/files/id/165739
