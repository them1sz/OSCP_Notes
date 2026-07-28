# Methodology

#### Initial Domain Access

1. WinRM
2. Kerberoast with WinRM User&#x20;
3. ASREP Roast with WinRM User
4. Run BloodHound with WinRM User

#### After Privilege Escalation on First Box

1. Run mimikatz and dump `logonpasswords`
2. Run mimikatz and dump LSASS
3. Try to crack ALL NTLM hashes extracted from LSASS

#### Password Spray Everywhere

1. SMB with Domain & Local credentials for all users&#x20;
2. winRM with Domain & Local credentials for all users&#x20;
3. MSSQL with (Windows Auth) & local credentials & `sa` user&#x20;
