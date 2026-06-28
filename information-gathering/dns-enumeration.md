# DNS Enumeration

| Record | Purpose |
|---|---|
| `NS` | Authoritative nameservers for the domain |
| `A` | IPv4 address of a hostname |
| `AAAA` | IPv6 address of a hostname |
| `MX` | Mail exchange servers |
| `PTR` | Reverse lookups (IP → hostname) |
| `CNAME` | Alias records |
| `TXT` | Arbitrary text (ownership verification, SPF, etc.) |

**Tools:** `host`, `dig`, `dnsrecon`, `dnsenum`

**Bruteforce alive subdomains (bash):**
```bash
for sub in $(cat subdomains.txt); do host $sub.<target.com>; done
```

**Reverse DNS lookups across a range:**
```bash
for octet in $(seq 200 254); do host 51.222.169.$octet; done | grep -vi "not found"
```
