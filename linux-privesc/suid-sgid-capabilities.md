# Finding Files

**SUID binaries:**

```bash
find / -perm -u=s -type f 2>/dev/null
find / -perm -4000 2>/dev/null
```

**SGID binaries:**

```bash
find / -perm -2000 2>/dev/null
```

**Capabilities:**

```bash
/usr/sbin/getcap -r / 2>/dev/null
```

> Use [GTFOBins](https://gtfobins.github.io) for exploitation of misconfigured SUID/capability binaries.

> If GTFOBins exploit throws access denied, check `/var/log/syslog` to identify what failed.

#### Readable/Writable files of a specific group

```bash
find / -group user -perm -g=w 2>/dev/null
```

### Executable Files Owned by Root&#x20;

```bash
find / -type f -user root -name *.sh 2>/dev/null
```

```bash
# ALL PERMS
find / -perm -777 -type f 2>/dev/null

# Writables for current user/group
find / perm /u=w -user `whoami` 2>/dev/null
find / -perm /u+w,g+w -f -user `whoami` 2>/dev/null
find / -perm /u+w -user `whoami` 2>/dev/nul

# Dirs with +w perms for current u/g
find / perm /u=w -type -d -user `whoami` 2>/dev/null
find / -perm /u+w,g+w -d -user `whoami` 2>/dev/null
```
