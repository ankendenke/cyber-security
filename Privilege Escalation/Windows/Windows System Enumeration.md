Gather Windows System Information
```
systeminfo
```

Select OS Name, OS Version, System Type
```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

Host Name
```
hostname
```

Check Update and Hotfixes
```
wmic qfe
```

Select a subset info of Hotfixes
```
wmic qfe get Caption,Description,HotfixID,Installation
```

List all the drives (messy output :))
```
wmic logicaldisk
```
Select subset info
```
wmic logicaldisk get caption,description,providername
```
```
C:\Users\medtr>wmic logicaldisk get caption,description,providername
Caption  Description       ProviderName
C:       Local Fixed Disk
D:       Removable Disk
G:       Local Fixed Disk
```
