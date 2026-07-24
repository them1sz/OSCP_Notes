# Socat Dynamic Tunneling

```bash
socat -ddd TCP-LISTEN:2345,fork TCP:<compromised-host-ip>:<target-port>
```

* `-ddd` — verbose output
* `fork` — handle multiple connections (don't die after first)
* Sets up a listener on port 2345 on the compromised machine. Everything sent to 2345 (e.g., from the attacker's machine) is forwarded to the target port on the compromised host.

