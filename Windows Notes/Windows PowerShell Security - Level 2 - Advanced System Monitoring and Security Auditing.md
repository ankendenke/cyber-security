[[Windows]]
# 1. Event Log Analysis Functions
```powershell
function Get-SecurityEvents {
    param (
        [int]$Hours = 24,
        [int]$MaxEvents = 50
    )
    Write-Host "`n=== Recent Security Events ===" -ForegroundColor Cyan
    Get-WinEvent -FilterHashtable @{
        LogName = 'Security'
        Level = 2,3
        StartTime = (Get-Date).AddHours(-$Hours)
    } -MaxEvents $MaxEvents | Select-Object TimeCreated, Id, LevelDisplayName, Message
}
```

# 2. Advanced Process Monitoring
```powershell
function Get-SuspiciousProcesses {
    Write-Host "`n=== Suspicious Process Detection ===" -ForegroundColor Cyan
    
    # Get all running processes with their properties
    $processes = Get-Process | Select-Object Name, Id, Path, Company, CPU, WorkingSet
    
    # Look for processes with high CPU usage or no company name
    $suspicious = $processes | Where-Object {
        $_.CPU -gt 50 -or [string]::IsNullOrEmpty($_.Company)
    }
    
    # Display results
    $suspicious | Format-Table -AutoSize
}

```
# 3. Network Security Analysis
```powershell
function Get-NetworkSecurityStatus {
    Write-Host "`n=== Network Security Analysis ===" -ForegroundColor Cyan
    
    # Check firewall status
    Write-Host "Firewall Status:" -ForegroundColor Yellow
    Get-NetFirewallProfile | Select-Object Name, Enabled
    
    # Check active connections
    Write-Host "`nActive Connections:" -ForegroundColor Yellow
    Get-NetTCPConnection -State Established |
        Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State |
        Format-Table -AutoSize
    
    # Check listening ports
    Write-Host "`nListening Ports:" -ForegroundColor Yellow
    Get-NetTCPConnection -State Listen |
        Select-Object LocalAddress, LocalPort, State |
        Format-Table -AutoSize
}

```
# 4. User Account Monitoring
```powershell
function Get-UserSecurityAudit {
    Write-Host "`n=== User Account Security Audit ===" -ForegroundColor Cyan
    
    # Get local users and their properties
    Write-Host "Local User Accounts:" -ForegroundColor Yellow
    Get-LocalUser | Select-Object Name, Enabled, LastLogon, PasswordRequired, 
                    PasswordLastSet, PasswordExpires |
    Format-Table -AutoSize
    
    # Get admin group members
    Write-Host "`nAdministrator Group Members:" -ForegroundColor Yellow
    Get-LocalGroupMember -Group "Administrators" |
        Select-Object Name, PrincipalSource
}
```

# 5. File System Security Monitor
```powershell
function Start-FileSystemMonitor {
    param (
        [string]$Path = "C:\Windows\System32",
        [int]$Duration = 60  # Duration in seconds
    )
    Write-Host "`n=== File System Security Monitor ===" -ForegroundColor Cyan
    Write-Host "Monitoring $Path for changes... (Duration: $Duration seconds)"
    
    $fsw = New-Object System.IO.FileSystemWatcher
    $fsw.Path = $Path
    $fsw.IncludeSubdirectories = $true
    $fsw.EnableRaisingEvents = $true
    
    # Create event handlers
    $action = {
        $details = $event.SourceEventArgs
        $name = $details.Name
        $changeType = $details.ChangeType
        $timestamp = $event.TimeGenerated
        Write-Host "[$timestamp] $changeType : $name" -ForegroundColor Yellow
    }
    
    # Register event handlers
    $handlers = . {
        Register-ObjectEvent -InputObject $fsw -EventName Created -Action $action
        Register-ObjectEvent -InputObject $fsw -EventName Deleted -Action $action
        Register-ObjectEvent -InputObject $fsw -EventName Changed -Action $action
    }
    
    # Monitor for specified duration
    Start-Sleep -Seconds $Duration
    
    # Cleanup
    $handlers | ForEach-Object {
        Unregister-Event -SourceIdentifier $_.Name
    }
    $fsw.Dispose()
}
```

# Main execution menu
```powershell
function Show-SecurityMenu {
    Write-Host "`n=== Security Monitoring Menu ===" -ForegroundColor Green
    Write-Host "1. Check Recent Security Events"
    Write-Host "2. Monitor Suspicious Processes"
    Write-Host "3. Analyze Network Security"
    Write-Host "4. Audit User Accounts"
    Write-Host "5. Monitor File System"
    Write-Host "6. Run All Checks"
    Write-Host "Q. Quit"
}

```
# Interactive menu
```powershell
do {
    Show-SecurityMenu
    $choice = Read-Host "`nSelect an option"
    
    switch ($choice) {
        "1" { Get-SecurityEvents }
        "2" { Get-SuspiciousProcesses }
        "3" { Get-NetworkSecurityStatus }
        "4" { Get-UserSecurityAudit }
        "5" { Start-FileSystemMonitor }
        "6" { 
            Get-SecurityEvents
            Get-SuspiciousProcesses
            Get-NetworkSecurityStatus
            Get-UserSecurityAudit
            Start-FileSystemMonitor -Duration 30
        }
        "Q" { return }
        Default { Write-Host "Invalid option" -ForegroundColor Red }
    }
} while ($true)
```