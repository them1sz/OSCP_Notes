# NetBIOS & SMB

* **NetBIOS:** TCP port 139 (also UDP); often enabled alongside SMB for backward compatibility.
* **SMB:** TCP port 445.

```bash
# NetBIOS scan
sudo nbtscan -r <subnet>
```

### **SMB enumeration (cmd)**

```cmd
net view                  # list machines visible to this host
net view /domain          # list domains and workgroups
net view \\dc1 /all       # list all shares on dc1 (admin shares end with $)
```

**Automation tools:** `enum4linux`, `nxc` (NetExec/CrackMapExec replacement)

### Enum4Linux - Unauthenticated recon

```bash
## Works best when guest access or null authentication in a share is supported
## Gathers various information (password policy, domain info etc)
## By default it runs all checks 
enum4linux <domain-joined-ip-address>
```

### Connect to a specific share authenticated

```bash
smbclient //172.16.129.83/C -U medtech.com/wario%Mushroom!
```

