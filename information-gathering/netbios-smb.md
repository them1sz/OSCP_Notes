# NetBIOS & SMB

- **NetBIOS:** TCP port 139 (also UDP); often enabled alongside SMB for backward compatibility.
- **SMB:** TCP port 445.

```bash
# NetBIOS scan
sudo nbtscan -r <subnet>
```

**Windows SMB enumeration:**
```cmd
net view                  # list machines visible to this host
net view /domain          # list domains and workgroups
net view \\dc1 /all       # list all shares on dc1 (admin shares end with $)
```

**Automation tools:** `enum4linux`, `nxc` (NetExec/CrackMapExec replacement)
