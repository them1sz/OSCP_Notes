# Port Scanning

### **Netcat**&#x20;

**TCP scan**

```bash
for port in $(seq 1 1000); do nc -nvvz -w 1 <ip> $port; done 
```

**UDP scan**

```bash
for port in $(seq 1 100); do nc -nvvzu -w 1 <ip> $port; done
```

### NMAP scanning

```bash
# Host discovery ping sweep
sudo nmap -sn 192.168.50.0/24 -oA sweep-scan -vv

# Full TCP scan with performance flags
sudo nmap -sS -p- --max-retries 2 --min-rate 1000 <ip>

# Combined TCP + UDP
sudo nmap -sS -sU <ip>
```

#### **Useful Nmap flags**

* `--min-rate 1000` — enforces minimum probe rate (overrides congestion throttling)
* `--max-rtt-timeout 200ms` — cap wait time on unresponsive ports
* `--max-retries 2` — stop reprobing non-responsive ports
* `--min-hostgroup 16` — process more hosts concurrently

> When nmap throttles (you see "Increasing send delay" messages), rerun with `--min-rate 1000 --max-retries 2`.

#### &#x20;NMAP NSE Engine scripts&#x20;

`/usr/share/nmap/scripts/`&#x20;

Run a specific script or all scripts `sudo nmap --script="smtp-*" 192.168.182.189`

### Nmap over socks5 proxy

```bash
sudo nmap -sT -v -n <ip-address> -oN scan.nmap -Pn
```

### **PowerShell**&#x20;

```powershell
# Single port
Test-NetConnection -Port 445 192.168.50.151

# Ports 1–1024
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```
