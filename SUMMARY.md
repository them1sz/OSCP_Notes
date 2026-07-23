# Table of contents

## OSCP-B

## Information Gathering

* [GitHub Recon](README.md)
* [DNS Enumeration](information-gathering/dns-enumeration.md)
* [NetBIOS & SMB](information-gathering/netbios-smb.md)
* [Port Scanning](information-gathering/port-scanning.md)
* [SMTP Enumeration](information-gathering/smtp-enumeration.md)
* [SNMP Enumeration](information-gathering/snmp-enumeration.md)
* [WordPress Scanning](information-gathering/wordpress-scanning.md)
* [NXC - Net Exec](information-gathering/nxc-net-exec.md)
* [Interesting Filesystem folders](information-gathering/interesting-filesystem-folders.md)
* [Exploit URLs](information-gathering/exploit-urls.md)
* [Finding Exploits](information-gathering/finding-exploits.md)

## Web Attacks

* [Path Traversal](web-attacks/path-traversal.md)
* [LFI / RFI](web-attacks/lfi-rfi.md)
* [File Upload](web-attacks/file-upload.md)
* [Command Injection](web-attacks/command-injection.md)

## SQL Injection

* [MySQL](sql-injection/mysql.md)
* [MSSQL](sql-injection/mssql.md)
* [PostgreSQL](sql-injection/postgresql.md)

## Windows Privilege Escalation

* [Preliminary Recon](windows-privesc/initial-enumeration.md)
* [Service Binary Hijacking](windows-privesc/service-binary-hijacking.md)
* [DLL Hijacking](windows-privesc/dll-hijacking.md)
* [Unquoted Service Paths](windows-privesc/unquoted-service-paths.md)
* [Scheduled Tasks](windows-privesc/scheduled-tasks.md)
* [Special Privileges](windows-privesc/special-privileges.md)
* [Automation](windows-privilege-escalation/automation.md)

## Linux Privilege Escalation

* [Initial Enumeration](linux-privesc/initial-enumeration.md)
* [Cron Jobs & Services](linux-privesc/cron-jobs-services.md)
* [Password Files](linux-privesc/password-files.md)
* [Searching for files](linux-privesc/suid-sgid-capabilities.md)
* [Sudo Abuse](linux-privesc/sudo-abuse.md)
* [Kernel Exploits](linux-privesc/kernel-exploits.md)

## Password Attacks

* [Brute Force Attacks](password-attacks/brute-force.md)
* [Hash Cracking](password-attacks/hash-cracking.md)
* [Mimikatz & Windows Hashes](password-attacks/mimikatz-windows-hashes.md)
* [Pass-the-Hash](password-attacks/pass-the-hash.md)
* [Net-NTLMv2, Responder & Relay](password-attacks/ntlmv2-responder-relay.md)

## Active Directory

* [Key Concepts & Architecture](active-directory/key-concepts.md)
* [Preliminary Recon](active-directory/enumeration.md)
* [BloodHound](active-directory/bloodhound.md)
* [Share Enumeration](active-directory/share-enumeration.md)
* [Note dump](active-directory/note-dump.md)

## File Transfers

* [File Transfering & Downloading](file-transfers/capstone-notes.md)

## Reverse Shells

***

* [Various Reverse Shells](various-reverse-shells.md)

## Authentication Attacks

* [Password Spraying](active-directory/auth-attacks/password-spraying.md)
* [AS-REP Roasting](active-directory/auth-attacks/asrep-roasting.md)
* [Kerberoasting](active-directory/auth-attacks/kerberoasting.md)
* [Silver Tickets](active-directory/auth-attacks/silver-tickets.md)
* [DCSync](active-directory/auth-attacks/dcsync.md)

## Lateral Movement

* [WMI / WinRM / PsExec](active-directory/lateral-movement/wmi-winrm-psexec.md)
* [Pass / Over-Pass / Pass-the-Ticket](active-directory/lateral-movement/pass-overpass-ticket.md)
* [DCOM](active-directory/lateral-movement/dcom.md)

## Port Forwarding & Tunneling

* [Socat](port-forwarding/socat.md)
* [SSH Tunneling](port-forwarding/ssh-tunneling.md)
* [sshuttle](port-forwarding/sshuttle.md)
* [Chisel](port-forwarding/chisel.md)
* [Windows (Plink / Netsh)](port-forwarding/windows-plink-netsh.md)

## AV Evasion

* [AV Evasion](av-evasion.md)

## Linux Basics

* [Linux Basics](linux-basics.md)

## Persistence

* [Golden Tickets](active-directory/persistence/golden-tickets.md)
* [Shadow Copies (NTDS.dit)](active-directory/persistence/shadow-copies.md)
