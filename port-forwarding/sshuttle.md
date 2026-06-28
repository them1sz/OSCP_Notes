# sshuttle

Acts like a VPN over SSH. Routes all traffic for specified subnets through the tunnel.

**Requirements:** Root on SSH client; Python3 on SSH server.

```bash
# If using socat to forward SSH first:
socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22

# sshuttle — route traffic for two subnets
sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
```

After this, reach internal subnets directly from Kali without proxychains.
