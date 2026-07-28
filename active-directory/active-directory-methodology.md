# Active Directory Methodology

### Recon steps as low - priv user

```
enum4linux ? 
ldapdomaindump ? 

# Check SYSVOL through SMB to DC
\\dc1.corp.com\sysvol\corp.com\ 
# In case any policy is found
gpp-decrypt <cpassword-value>



```

