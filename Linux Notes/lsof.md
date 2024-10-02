[[Linux]] command to monitor file opened on the local system
# Using LSOF for Linux Incident Response
## Introduction
`lsof` (List Open Files) is a powerful command-line utility for incident response and forensics in Linux environments. It provides critical information about files that are opened by various processes, including network connections, running executables, and file handlers.

## Basic Syntax
```bash
lsof [options] [names]
```

## Essential LSOF Commands for Incident Response

### 1. Identify All Network Connections
```bash
# List all network connections
lsof -i

# List only TCP connections
lsof -i TCP

# List only listening ports
lsof -i -P -n | grep LISTEN
```

### 2. Process Investigation
```bash
# List all files opened by a specific process ID
lsof -p <PID>

# Find all processes running from a specific directory
lsof +D /path/to/directory

# List all files opened by a specific user
lsof -u username
```

### 3. Port Analysis
```bash
# Check specific port usage
lsof -i :<port_number>

# Monitor all ports below 1024
lsof -i :1-1024
```

## Advanced Incident Response Techniques

### 1. Identifying Suspicious File Access
```bash
# Monitor file access in real-time
watch -n 1 "lsof | grep /suspicious/path"

# Find deleted but still open files
lsof +L1
```

### 2. Memory Analysis
```bash
# List all memory-mapped files
lsof -d mem

# Show memory maps of a specific process
lsof -p <PID> -d mem
```

### 3. Network Forensics
```bash
# Track all IPv4 connections
lsof -i 4

# Track all IPv6 connections
lsof -i 6

# Monitor established connections
lsof -i -s TCP:ESTABLISHED
```

## Common Incident Response Scenarios

### Scenario 1: Potential Data Exfiltration
```bash
# Monitor all outbound connections
lsof -i -n | grep ESTABLISHED

# Check for large open files
lsof -s | grep 'GB'
```

### Scenario 2: Malware Investigation
```bash
# Find hidden processes
lsof -p $(pgrep -d,) | grep -i 'deleted'

# Check for suspicious network connections
lsof -i -n -P | grep -v LISTEN | grep -v ESTABLISHED
```

### Scenario 3: Rootkit Detection
```bash
# Look for hidden files in /proc
lsof -p $(pgrep -d,) | grep '/proc'

# Check for files with no links
lsof +L0
```

## Best Practices for Incident Response

1. **Documentation**
   - Always document the commands used and their output
   - Use `-n` flag to prevent DNS lookups which might alter evidence
   - Timestamp all command outputs

2. **Evidence Preservation**
   ```bash
   # Save lsof output with timestamp
   lsof [options] > "lsof_$(date +%Y%m%d_%H%M%S).log"
   ```

3. **Performance Considerations**
   - Use specific filters to reduce system load
   - Avoid running resource-intensive commands on production systems
   - Consider using `-r` for periodic monitoring instead of continuous loops

## Important Flags for Incident Response

| Flag | Description | Use Case |
|------|-------------|----------|
| `-i` | Network connections | Identify malicious connections |
| `-p` | Process specific | Investigate suspicious processes |
| `-u` | User specific | Track user activity |
| `-r` | Repeat mode | Continuous monitoring |
| `-t` | Terse output | Scripts and automation |
| `-n` | No DNS resolution | Prevent network artifacts |

## Common Pitfalls to Avoid

1. Running intensive queries without proper filtering
2. Forgetting to preserve evidence
3. Not considering the impact on system resources
4. Overlooking deleted but open files
5. Missing hidden network connections

## Emergency Response Checklist

1. [ ] Capture current network connections
2. [ ] Document suspicious processes
3. [ ] Check for deleted but open files
4. [ ] Monitor specific directories for changes
5. [ ] Record all findings with timestamps
6. [ ] Look for unauthorized elevated privileges
7. [ ] Check for hidden network ports