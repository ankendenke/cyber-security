As a security researcher, understanding the `findstr` command in [[Windows]] can be valuable for various tasks, from basic log analysis to more advanced threat hunting. Let's explore some examples of how you can use `findstr`, progressing from beginner to more advanced usage.

Beginner level:

1. Basic string search in a file:
```
findstr "error" log.txt
```
This searches for the word "error" in log.txt and displays all lines containing it.

2. Case-insensitive search:
```
findstr /i "password" config.ini
```
Searches for "password" in config.ini, ignoring case.

Intermediate level:

3. Searching multiple files:
```
findstr /s /i "malware" C:\*.log
```
Recursively searches all .log files in C:\ for "malware", ignoring case.

4. Using regular expressions:
```
findstr /r "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" access.log
```
Searches for IP address patterns in access.log.

5. Excluding lines:
```
findstr /v "SYSTEM" security.evt
```
Displays all lines from security.evt that don't contain "SYSTEM".

Advanced level:

6. Combining multiple search patterns:
```
findstr /c:"failed login" /c:"unauthorized access" /c:"brute force attempt" auth.log
```
Searches for multiple specific phrases in auth.log.

7. Piping with other commands:
```
type iis.log | findstr "POST" | findstr /v "200 OK"
```
Finds all POST requests in iis.log that didn't return a 200 OK status.

8. Using findstr in a batch script for threat hunting:
```batch
@echo off
for %%F in (C:\Windows\System32\*.dll) do (
    findstr /m "CreateRemoteThread" "%%F" >nul
    if not errorlevel 1 (
        echo Potential suspicious DLL: %%F
    )
)
```
This script searches all DLLs in System32 for the string "CreateRemoteThread", which could indicate potential malicious activity.

Pro level:

9. Combining with PowerShell for advanced log analysis:
```powershell
Get-ChildItem -Path C:\Logs -Recurse -Filter *.log | 
ForEach-Object {
    $file = $_.FullName
    $content = Get-Content $file | findstr /r /c:"^Error" /c:"^Warning"
    if ($content) {
        Write-Output "Found in $file:"
        $content
    }
}
```
This PowerShell script uses `findstr` to search for lines starting with "Error" or "Warning" in all .log files recursively.

10. Using findstr in a live incident response scenario:
```batch
for /f "tokens=2 delims=:" %%a in ('findstr /m /c:"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" C:\Windows\System32\config\SYSTEM') do (
    echo Potential persistence mechanism found in registry: %%a
)
```
This command searches the SYSTEM registry hive for potential persistence mechanisms in the Run key.

These examples demonstrate how `findstr` can be a powerful tool for security researchers, from basic log searching to complex threat hunting scenarios. As you become more proficient, you can combine `findstr` with other Windows commands, PowerShell, and custom scripts to create sophisticated security analysis tools.