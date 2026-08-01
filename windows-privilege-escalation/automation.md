# Automation

### WinPeasx64

```c
winPEASx64.exe servicesinfo > servicesinfo.txt : Only service missconfigurations

winPEASx64.exe systeminfo > systeminfo.txt : Local exploit suggestions 

winPEASx64.exe networkinfo > netwrokinfo.txt : Network info 


## In order to have the results appended to a file while at the same time save them to a file
.\winpeas.exe | Tee-Object -FilePath results.txt
```

### PrivescCheck.ps1

```
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended"
```



