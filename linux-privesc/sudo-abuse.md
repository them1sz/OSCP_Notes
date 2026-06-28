# Abusing Sudo

```bash
sudo -l      # list what current user can run as sudo
```

**Example sudoers entry:**
```
(root) NOPASSWD: /usr/bin/vim
```
Means: user can run `vim` as root with no password → escape to shell via `:!/bin/bash`.

Edit sudoers safely: `sudo visudo`
