# WordPress Scanning

```bash
wpscan --no-update --url http://192.168.110.244/ --random-user-agent -v \
  --api-token ajdZfYu1QPaKraHyM377YAWilYpG0xPk8QTSw5e9B3k \
  --enumerate vp,vt,cb,u,m \
  --plugins-detection aggressive | tee -a wpscan.txt
```
