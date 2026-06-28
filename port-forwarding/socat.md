# Socat Port Forwarding

```bash
socat -ddd TCP-LISTEN:2345,fork TCP:10.4.50.215:5432
```
- `-ddd` — verbose output
- `fork` — handle multiple connections (don't die after first)
- Forwards all traffic received on 2345 → target:5432
