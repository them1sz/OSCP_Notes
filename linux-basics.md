# Linux Basics

## File Permissions

```
-rw-r--r--    owner: rw- | group: r-- | others: r--
drwxrwx---    owner: rwx | group: rwx | others: ---
```

**Octal notation:** `r=4, w=2, x=1` → `777` = rwx for all, `644` = rw-r--r--

**Special bits:**

- **SUID (4000):** Executable runs as the file owner's UID
  ```bash
  find / -perm -4000 2>/dev/null
  find / -perm -u=s 2>/dev/null
  ```
- **SGID (2000):** Executable runs with the file's group GID; directories make new files inherit group ownership
  ```bash
  find / -perm -2000 2>/dev/null
  ```
- **Sticky Bit (1000):** Only file owner/dir owner/root can delete files in the directory (e.g., `/tmp`)
  ```bash
  find / -perm -1000 2>/dev/null
  ```

---

## Sudoers File

```bash
sudo visudo    # safe editor for sudoers
sudo -l        # list current user's sudo permissions
```

**Example entry:**
```
(root) NOPASSWD: /usr/bin/vim
```
This allows running `vim` as root with no password → `vim` `:!/bin/bash` → root shell.
