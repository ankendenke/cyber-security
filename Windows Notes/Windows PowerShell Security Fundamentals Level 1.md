[[Windows]]

# 1. Basic Commands and Pipeline
# Get-Command: Lists available commands
```powershell
Get-Command -Name "*security*"  # Lists security-related commands
```

# Variables and Data Types
```powershell
$computerName = $env:COMPUTERNAME
$currentUser = $env:USERNAME
$timestamp = Get-Date

```
# Basic Output
```powershell
Write-Host "=== System Security Audit ===" -ForegroundColor Green
Write-Host "Computer: $computerName"
Write-Host "User: $currentUser"
Write-Host "Timestamp: $timestamp"
```

# 2. Basic System Information Collection
```powershell
function Get-BasicSecurityInfo {
    # Operating System Details
    $os = Get-WmiObject -Class Win32_OperatingSystem
    Write-Host "`nOperating System Information:" -ForegroundColor Cyan
    Write-Host "OS Version: $($os.Version)"
    Write-Host "Last Boot: $($os.ConvertToDateTime($os.LastBootUpTime))"
    
    # Antivirus Status (Windows Defender)
    Write-Host "`nAntivirus Status:" -ForegroundColor Cyan
    Get-Service -Name WinDefend | Select-Object Name, Status
}
```

# 3. Simple File Operations
```powershell
function Test-FilePermissions {
    param (
        [string]$path = "C:\Windows\System32"
    )
    
    Write-Host "`nChecking File Permissions for: $path" -ForegroundColor Cyan
    Get-Acl $path | Select-Object Owner, AccessToString
}

```
# 4. Basic Error Handling
```powershell
function Test-SecurityFunction {
    try {
        Get-Service -Name "NonExistentService"
    }
    catch {
        Write-Host "Error occurred: $($_.Exception.Message)" -ForegroundColor Red
    }
}

```
# Execute functions
```powershell
Get-BasicSecurityInfo
Test-FilePermissions
Test-SecurityFunction
```