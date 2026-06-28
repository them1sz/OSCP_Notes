# Key Concepts & Architecture

## Hash Types

**NT Hash:** Cryptographic representation of the password stored in SAM/NTDS.dit. Used in PtH attacks.

**Net-NTLMv2 Hash:** Generated on-the-fly during network authentication (challenge-response). Cannot be used for PtH — but can be captured (Responder), relayed, or cracked offline.

---

## Authentication

**Authentication by address vs. hostname:**
- IP address → forces **NTLM** authentication
- Hostname → attempts **Kerberos** first (supports delegation)

> **Kerberos Double Hop Problem:** When you authenticate via WinRM/PowerShell Remoting, your credentials are not forwarded to a third machine. Use RDP to avoid this during domain enumeration.

---

## AD Architecture

- **Domain Controller (DC):** Central hub storing all OUs, objects, and attributes. Also typically hosts DNS.
- **Domain Admins:** Complete control over the domain.
- **Enterprise Admins:** Full control over all domains in the forest.
- **Organizational Units (OUs):** Containers for organizing AD objects.
- **LDAP:** Protocol used to communicate with AD.

**LDAP path format:** `LDAP://HostName[:PortNumber][/DistinguishedName]`

**Distinguished Name example:**
```
CN=Stephanie,CN=Users,DC=corp,DC=com
```
Read right-to-left: domain (corp.com) → parent container (Users) → object (Stephanie).
