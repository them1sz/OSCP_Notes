# Windows Port Forwarding

## Plink.exe (PuTTY command-line — remote forward)

```cmd
C:\Windows\Temp\plink.exe -ssh -l kali -pw <PASSWORD> -R 127.0.0.1:9833:127.0.0.1:3389 192.168.118.4
```

---

## Netsh (native — requires admin)

```powershell
# Add port forward rule
netsh interface portproxy add v4tov4 listenport=2222 listenaddress=192.168.50.64 connectport=22 connectaddress=10.4.50.215

# Confirm
netsh interface portproxy show all

# Open firewall
netsh advfirewall firewall add rule name="port_forward_ssh_2222" protocol=TCP dir=in localip=192.168.50.64 localport=2222 action=allow

# Cleanup
netsh advfirewall firewall delete rule name="port_forward_ssh_2222"
```
