# Hash Cracking

## Hash Identification

```bash
hashid <hash>
hash-identifier
```

---

## Hashcat Rules

```bash
# Append '1' to every password
echo \$1 > demo.rule
hashcat -r demo.rule --stdout wordlist.txt   # test rule output

# Available rule sets
ls -la /usr/share/hashcat/rules/

# Example: enforce password policy ending with 1@3$5
echo -n "\$1 \$@ \$3 \$\$ \$5" > policy.rule
hashcat -m 0 md5-hash -r policy.rule /usr/share/wordlists/rockyou.txt --force

# Show cracked
hashcat -m 0 md5-hash --show
```

**Rule function reference:**
- `$X` — append character X
- `^X` — prepend character X
- `u` — uppercase all
- `d` — duplicate password

---

## JtR Custom Rules

```text
# File: sshrules
[List.Rules:sshrules]
c $1 $3 $7 $!
c $1 $3 $7 $@
c $1 $3 $7 $#
```
Append to `/etc/john/john.conf`, then use:
```bash
john --rules=sshrules --wordlist=wordlist.txt hash.txt
```

---

## KeePass Database Cracking

```bash
# Find the .kdbx file
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

# Extract hash
keepass2john Database.kdbx > keepass.hash
# Remove "Database:" prefix from hash, then crack:
hashcat -m 13400 keepass.hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/rockyou-30000.rule --force
```

> `rockyou-30000.rule` is specifically designed for use with `rockyou.txt`.

---

## SSH Passphrase Cracking

```bash
ssh2john id_rsa > ssh.hash
john --wordlist=/usr/share/wordlists/rockyou.txt ssh.hash
```
