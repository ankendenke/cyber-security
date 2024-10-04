
## Overview
Privilege escalation occurs when a user or process gains higher-level permissions than they were intended to have. This can happen through:
- Vertical escalation (gaining higher privileges)
- Horizontal escalation (gaining same-level access as other users)

## Common Attack Vectors

### 1. Missing System Updates
- Unpatched vulnerabilities in OS and applications
- Legacy system components with known vulnerabilities

### 2. Misconfigured Permissions
- Overly permissive file/folder permissions
- Weak service account configurations
- Misconfigured sudo rights

### 3. Credential Issues
- Password reuse
- Plaintext credentials in files
- Hardcoded credentials in scripts

## Detection Strategies

### 1. Monitoring & Logging
- Monitor privilege changes
- Track sudo/admin command usage
- Log authentication attempts
- Monitor file permission changes

### 2. System Auditing
- Regular permission audits
- Service account reviews
- Configuration assessments
- File integrity monitoring

## Prevention Measures

### 1. System Hardening
- Regular patching schedule
- Remove unnecessary services
- Implement least privilege principle
- Use secure configurations

### 2. Access Control
- Implement Role-Based Access Control (RBAC)
- Regular access reviews
- Strong password policies
- Multi-factor authentication

### 3. Technical Controls
```bash
# Example configuration hardening
# Set correct permissions on sensitive directories
chmod 750 /etc/shadow
chmod 750 /etc/sudoers
chmod 700 /root

# Remove SUID from unnecessary binaries
find / -perm /4000 -type f -exec ls -ld {} \; | review_and_remove

# Limit sudo access
visudo
# Add specific commands instead of ALL
username ALL=(ALL) /specific/command
```

### 4. Policy Implementation
- Clear escalation procedures
- Regular security training
- Incident response plans
- Change management processes

## Monitoring Tools
- Auditd
- Sysmon
- OpenVAS
- Security Onion
- Wazuh

## Response Plan
1. Detect suspicious activity
2. Isolate affected systems
3. Investigate escalation path
4. Remediate vulnerabilities
5. Update security controls
6. Document and learn

## Regular Maintenance
- Schedule regular audits
- Update security policies
- Conduct penetration testing
- Review system logs
- Update training materials