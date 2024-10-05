[[Windows Privilege Escalation]]
## Overview
The "Potato" family of attacks (including Hot Potato, Sweet Potato, Rotten Potato, etc.) exploit Windows token impersonation mechanisms. These attacks target privilege escalation through manipulation of NTLM authentication and token impersonation.

## Technical Components
1. **Core Mechanisms Exploited**:
   - NTLM authentication relaying
   - Token impersonation privileges
   - Windows service behavior
   - Named pipe manipulation
   - COM server vulnerabilities

2. **Privilege Requirements**:
   - SeImpersonatePrivilege or SeAssignPrimaryPrivilege
   - Usually available to service accounts
   - Default for IIS application pools

## Technical Analysis
### Authentication Flow
1. Local SYSTEM services authenticate to local RPC ports
2. Authentication attempts can be intercepted
3. Token impersonation occurs through:
   - Named pipe manipulation
   - Local RPC port redirection
   - NTLM authentication capture

### Common Vulnerable Configurations
1. Services running as SYSTEM
2. Default COM server configurations
3. Unpatched Windows systems
4. Misconfigured service accounts

## Detection Methods
1. **Process Monitoring**:
   - Unusual token impersonation events
   - Unexpected SYSTEM-level process creation
   - Anomalous service behavior

2. **Network Analysis**:
   - Local NTLM authentication attempts
   - Unusual RPC traffic patterns
   - Named pipe creation/manipulation

## Prevention Strategies
1. **System Hardening**:
   - Regular system updates
   - Proper service account configuration
   - Limited token privileges

2. **Configuration Changes**:
   - Disable unnecessary NTLM authentication
   - Implement strict service account policies
   - Monitor token usage

3. **Security Measures**:
   - Implement LAPS
   - Use Group Managed Service Accounts
   - Enable Windows Defender Credential Guard

## Incident Response
1. **Initial Response**:
   - Identify compromised accounts
   - Document affected systems
   - Isolate impacted services

2. **Investigation Steps**:
   - Review security logs
   - Analyze process creation events
   - Track token usage

## Mitigation Strategies
1. **Short-term**:
   - Apply available patches
   - Review service account privileges
   - Monitor for exploitation attempts

2. **Long-term**:
   - Implement Zero Trust architecture
   - Regular security assessments
   - Enhanced monitoring solutions

## Best Practices
1. **Service Configuration**:
   - Minimum required privileges
   - Regular privilege audits
   - Service account management

2. **System Management**:
   - Patch management
   - Configuration control
   - Security baseline enforcement

## Security Monitoring
1. **Key Indicators**:
   - Unexpected privilege escalation
   - Unusual token manipulation
   - Anomalous service behavior

2. **Logging Requirements**:
   - Process creation events
   - Token manipulation events
   - Service account activity