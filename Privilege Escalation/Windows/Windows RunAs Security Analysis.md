[[Windows Privilege Escalation]]
## Attack Vectors

### 1. Credential Harvesting
- Attackers can use tools to capture plaintext credentials when RunAs is executed from command line
- Malicious programs can hook into the RunAs process to intercept credentials
- Credentials may be logged in command history or log files

### 2. Token Manipulation
- Stolen tokens from RunAs sessions can be reused for lateral movement
- Token impersonation allows privilege escalation
- Abandoned RunAs processes may leave exposed tokens

### 3. Process Injection
- Attackers can inject malicious code into legitimate RunAs processes
- DLL injection into elevated RunAs processes enables privilege escalation
- Code injection into RunAs processes can bypass security controls

## Defense Strategies

### 1. Policy Controls
- Restrict RunAs usage through Group Policy
- Implement time limits on RunAs sessions
- Require specific security groups for RunAs privileges
- Log and audit all RunAs usage

### 2. Technical Controls
- Deploy endpoint detection and response (EDR) solutions to monitor RunAs activity
- Implement process creation monitoring
- Enable Windows Defender Credential Guard
- Use Protected Users security group for privileged accounts

### 3. Operational Security
- Require smart cards or Windows Hello for Business instead of passwords
- Train users on secure credential handling
- Implement Just-In-Time (JIT) administration
- Regular review of RunAs permissions and usage

### 4. Monitoring & Detection
- Monitor for suspicious RunAs patterns
- Track failed RunAs attempts
- Alert on off-hours RunAs usage
- Monitor for credential dumping tools

## Recommended Event IDs to Monitor
- 4624 (Account Logon)
- 4648 (Explicit Credential Logon)
- 4672 (Special Privileges Assigned)
- 4688 (Process Creation)
- 4689 (Process Termination)

## PowerShell Detection Script Example
```powershell
# Monitor for suspicious RunAs activity
$filter = @{
    LogName = 'Security'
    ID = 4648
    StartTime = (Get-Date).AddHours(-1)
}
Get-WinEvent -FilterHashtable $filter | 
    Where-Object { $_.Message -match 'runas' } |
    Select-Object TimeCreated, Message
```