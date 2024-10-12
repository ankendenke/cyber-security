Specific examples for each of the main use cases of the "net" command in [[Windows]]:

1. **User and group management**:

```
net user john /add
net user john NewPassword123
net localgroup Administrators john /add
net user jane /delete
```

These commands add a new user "john", set his password, add him to the Administrators group, and delete user "jane".

2. **Network resource management**:

```
net share
net share MyDocs=C:\Users\MyName\Documents /grant:Everyone,read
net use Z: \\server\shared_folder
net use Z: /delete
```

These list shared resources, create a new share, map a network drive, and delete a mapped drive.

3. **Service control**:

```
net start "Print Spooler"
net stop "Windows Update"
net pause "SQL Server (MSSQLSERVER)"
net continue "SQL Server (MSSQLSERVER)"
```

These start the Print Spooler service, stop Windows Update, pause SQL Server, and then resume it.

4. **Time synchronization:**

```
net time \\timeserver.example.com /set /yes
```

This synchronizes the local computer's time with a specified time server.

5. **Domain operations**:

```
net computer \\DESKTOP-ABC123 /add
net group "Domain Admins" /domain
```

These add a computer to the domain and list members of the Domain Admins group.
