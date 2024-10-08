[[Windows]]
# Basic Security Operations in PowerShell

# 1. Getting System Information
```powershell
function Get-BasicSystemInfo {
    Write-Host "`n=== System Information ===" -ForegroundColor Green
    $os = Get-WmiObject -Class Win32_OperatingSystem
    $computerSystem = Get-WmiObject -Class Win32_ComputerSystem
    
    Write-Host "OS Version: $($os.Version)"
    Write-Host "Computer Name: $($computerSystem.Name)"
    Write-Host "Last Boot Time: $($os.ConvertToDateTime($os.LastBootUpTime))"
}

```
# 2. Checking Running Processes
```powershell
function Get-ProcessInfo {
    Write-Host "`n=== Running Processes ===" -ForegroundColor Green
    Get-Process | Select-Object Name, ID, CPU | Sort-Object CPU -Descending | Select-First 5
}
```

# 3. Network Connections
```powershell
function Get-NetworkConnections {
    Write-Host "`n=== Active Network Connections ===" -ForegroundColor Green
    Get-NetTCPConnection | Where-Object State -eq 'Established' |
    Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State
}

```
# 4. Service Status
```powershell
function Get-SecurityServices {
    Write-Host "`n=== Security-Related Services ===" -ForegroundColor Green
    $securityServices = @('WinDefend', 'SecurityHealthService', 'Sense', 'EventLog')
    Get-Service -Name $securityServices | Select-Object Name, Status, StartType
}

```
# 5. User Account Information
```powershell
function Get-UserAccountInfo {
    Write-Host "`n=== User Account Information ===" -ForegroundColor Green
    Get-LocalUser | Select-Object Name, Enabled, LastLogon, PasswordRequired
}

# Main execution
```

```powershell
Get-BasicSystemInfo
Get-ProcessInfo
Get-NetworkConnections
Get-SecurityServices
Get-UserAccountInfo
```