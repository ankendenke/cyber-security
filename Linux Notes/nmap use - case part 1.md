# Advanced Nmap Usage Guide: From Beginner to Expert [[Linux]]

## Basic Reconnaissance (Level 1)

### 1. Basic Host Discovery
```bash
# Ping scan to find live hosts
nmap -sn 192.168.1.0/24

# Quick scan of most common ports
nmap -F 192.168.1.0/24
```

### 2. Simple Port Scanning
```bash
# TCP SYN scan (Default)
nmap -sS 192.168.1.100

# TCP Connect scan (More detailed but noisy)
nmap -sT 192.168.1.100

# UDP scan
nmap -sU 192.168.1.100
```

## Intermediate Techniques (Level 2)

### 3. Service and Version Detection
```bash
# Aggressive version detection
nmap -sV --version-intensity 5 192.168.1.100

# OS detection
nmap -O 192.168.1.100

# Combined version and OS detection
nmap -sV -O -p- 192.168.1.100
```

### 4. Script Scanning
```bash
# Default script scan
nmap -sC 192.168.1.100

# Vulnerability scanning
nmap --script vuln 192.168.1.100

# SQL injection vulnerability check
nmap --script http-sql-injection 192.168.1.100
```

## Advanced Techniques (Level 3)

### 5. Stealth Scanning
```bash
# Fragmented packets
nmap -f 192.168.1.100

# Timing template (paranoid)
nmap -T0 192.168.1.100

# Custom packet timing
nmap --min-parallelism 1 --max-parallelism 1 --min-rate 10 --max-rate 50 192.168.1.100
```

### 6. Firewall/IDS Evasion
```bash
# Decoy scanning
nmap -D RND:5 192.168.1.100

# Source port manipulation
nmap --source-port 53 192.168.1.100

# MAC address spoofing
nmap --spoof-mac Dell 192.168.1.100
```

## Expert Techniques (Level 4)

### 7. Advanced NSE Usage
```bash
# Custom NSE script timing
nmap --script-timeout 60s --script http-* 192.168.1.100

# Aggressive service detection with all NSE scripts
nmap -sV -sC --script-args aggressive=true 192.168.1.100

# Custom script parameters
nmap --script http-brute --script-args userdb=users.txt,passdb=passes.txt 192.168.1.100
```

### 8. Real-World Scenarios

#### Scenario 1: Initial Reconnaissance of a Corporate Network
```bash
# Comprehensive but stealthy scan
nmap -sS -sV -O -p- \
--min-rate 100 \
--max-retries 2 \
--script default,safe \
--randomize-hosts \
-T4 \
-oA corporate_scan \
10.0.0.0/24
```

#### Scenario 2: Web Application Security Assessment
```bash
# Web server focused scan
nmap -p80,443 \
--script "http-* and not http-brute*" \
--script-args http.useragent="Mozilla/5.0" \
--open \
-sV \
--version-intensity 5 \
target-webapp.com
```

#### Scenario 3: Internal Network Security Audit
```bash
# Comprehensive internal audit
nmap -sS -sV -O \
-p1-65535 \
--script "default or safe or auth or vuln" \
--script-timeout 30m \
--max-parallelism 1 \
--stats-every 30s \
-oX internal_audit \
192.168.0.0/16
```

## Best Practices and Tips

1. **Documentation**
   - Always use output options (-oA, -oX, -oN) for documentation
   - Include timestamps and scan parameters in file names

2. **Legal Compliance**
   - Always obtain proper authorization before scanning
   - Document scope and permissions
   - Avoid aggressive scanning of production systems

3. **Resource Management**
   - Use appropriate timing templates based on network capacity
   - Consider target system limitations
   - Monitor system load during intensive scans

4. **Stealth Considerations**
   - Balance speed vs. detectability
   - Use decoys and timing controls when needed
   - Consider network monitoring capabilities

## Advanced Troubleshooting

### Common Issues and Solutions

1. **Blocked Scans**
```bash
# Try alternative timing
nmap -T2 --max-retries 3 target

# Use different probe types
nmap -PS21,22,23,25,80,443 target
```

2. **False Positives/Negatives**
```bash
# Verify with multiple scan types
nmap -sS target
nmap -sT target
nmap -sA target
```

### Performance Optimization

1. **Large Network Scans**
```bash
# Optimize for large networks
nmap --min-hostgroup 64 --max-hostgroup 256 \
--min-parallelism 10 --max-parallelism 30 \
network/24
```

2. **Resource-Constrained Environments**
```bash
# Lightweight scanning
nmap --max-retries 1 --host-timeout 15m \
--max-scan-delay 1000ms target
```