# Initial Enumeration

```bash
ps aux                        # all running processes
route / routel                # routing table
netstat -ano / ss -anp        # active connections and listening ports
cat /etc/iptables/rules.v4    # firewall rules

ls -lha /etc/cron*            # cron jobs (daily/hourly/weekly/monthly)
crontab -l                    # current user's cron jobs

dpkg -l                       # installed packages (Debian)

find / -type d -writable 2>/dev/null       # writable directories
find / -perm -u=s -type f 2>/dev/null      # SUID binaries

mount                         # mounted filesystems
cat /etc/fstab                # filesystems mounted at boot
lsblk                         # all available disk blocks

lsmod                         # loaded kernel modules
/sbin/modinfo <module>        # info on specific module
```

---

## History, Environment & Dotfiles

```bash
env                 # environment variables (may contain credentials)
cat ~/.bashrc       # executed on new shell sessions — may expose vars
```
