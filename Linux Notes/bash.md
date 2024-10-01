# [[Linux]] Bash Scripting Guide for Cybersecurity Professionals

## 1. Beginner Level

### 1.1 Basic Script Structure
```bash
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

### 1.2 Variables
```bash
name="John"
echo "Hello, $name"
```

### 1.3 User Input
```bash
read -p "Enter your name: " user_name
echo "Hello, $user_name"
```

### 1.4 Conditional Statements
```bash
if [ "$user_name" == "admin" ]; then
    echo "Welcome, administrator!"
else
    echo "Access denied."
fi
```

### 1.5 Loops
```bash
for i in {1..5}; do
    echo "Iteration $i"
done
```

## 2. Intermediate Level

### 2.1 Functions
```bash
check_root() {
    if [ "$(id -u)" -ne 0 ]; then
        echo "This script must be run as root" >&2
        exit 1
    fi
}
```

### 2.2 File Operations
```bash
if [ -f "/etc/passwd" ]; then
    echo "The passwd file exists."
fi
```

### 2.3 Command Substitution
```bash
current_user=$(whoami)
echo "Current user: $current_user"
```

### 2.4 Error Handling
```bash
set -e  # Exit immediately if a command exits with a non-zero status
trap 'echo "An error occurred. Exiting..."; exit 1' ERR
```

### 2.5 Parsing Command-line Arguments
```bash
while getopts ":h:p:" opt; do
    case $opt in
        h) host="$OPTARG" ;;
        p) port="$OPTARG" ;;
        \?) echo "Invalid option: -$OPTARG" >&2; exit 1 ;;
    esac
done
```

## 3. Advanced Level (Cybersecurity Focus)

### 3.1 Network Scanning
```bash
#!/bin/bash

check_dependencies() {
    command -v nmap >/dev/null 2>&1 || { echo >&2 "nmap is required but not installed. Aborting."; exit 1; }
}

scan_network() {
    local network=$1
    echo "Scanning network: $network"
    nmap -sn "$network"
}

check_dependencies
scan_network "192.168.1.0/24"
```

### 3.2 Log Analysis
```bash
#!/bin/bash

analyze_logs() {
    local log_file=$1
    local pattern=$2
    echo "Analyzing $log_file for pattern: $pattern"
    grep "$pattern" "$log_file" | awk '{print $1,$2,$9}'
}

analyze_logs "/var/log/auth.log" "Failed password"
```

### 3.3 Automated Backup
```bash
#!/bin/bash

backup_dir="/path/to/backup"
source_dir="/path/to/source"

create_backup() {
    timestamp=$(date +"%Y%m%d_%H%M%S")
    backup_file="backup_$timestamp.tar.gz"
    tar -czf "$backup_dir/$backup_file" "$source_dir"
    echo "Backup created: $backup_file"
}

create_backup
```

### 3.4 System Hardening
```bash
#!/bin/bash

harden_ssh() {
    sed -i 's/^PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
    sed -i 's/^#MaxAuthTries 6/MaxAuthTries 3/' /etc/ssh/sshd_config
    systemctl restart sshd
    echo "SSH hardened"
}

disable_unused_services() {
    services_to_disable=("telnet" "rsh" "rlogin")
    for service in "${services_to_disable[@]}"; do
        systemctl disable "$service"
        systemctl stop "$service"
        echo "Disabled and stopped $service"
    done
}

harden_ssh
disable_unused_services
```

### 3.5 Intrusion Detection
```bash
#!/bin/bash

monitor_login_attempts() {
    tail -f /var/log/auth.log | while read line; do
        if echo "$line" | grep -q "Failed password"; then
            ip=$(echo "$line" | awk '{print $(NF-3)}')
            echo "Failed login attempt from IP: $ip"
            # Add IP to firewall block list
            iptables -A INPUT -s "$ip" -j DROP
        fi
    done
}

monitor_login_attempts
```

## 4. Pro Level (Advanced Cybersecurity Applications)

### 4.1 Automated Vulnerability Scanning
```bash
#!/bin/bash

run_vulnerability_scan() {
    local target=$1
    local output_file="vuln_scan_$(date +%Y%m%d).txt"
    
    echo "Running vulnerability scan on $target"
    nmap -sV --script vuln "$target" -oN "$output_file"
    echo "Scan complete. Results saved to $output_file"
}

run_vulnerability_scan "example.com"
```

### 4.2 Incident Response Automation
```bash
#!/bin/bash

incident_response() {
    local infected_system=$1
    
    echo "Initiating incident response for $infected_system"
    
    # Isolate the system
    ssh "$infected_system" "iptables -A INPUT -j DROP; iptables -A OUTPUT -j DROP"
    
    # Collect forensic data
    ssh "$infected_system" "netstat -tuln > netstat.txt; ps aux > processes.txt; lsof > open_files.txt"
    
    # Transfer logs
    scp "$infected_system:/var/log/*" ./incident_logs/
    
    echo "Initial incident response completed for $infected_system"
}

incident_response "compromised-server.local"
```

### 4.3 Continuous Security Monitoring
```bash
#!/bin/bash

monitor_system_changes() {
    local baseline_file="system_baseline.txt"
    local current_state_file="current_state.txt"
    
    if [ ! -f "$baseline_file" ]; then
        echo "Creating baseline..."
        find / -type f -exec md5sum {} + 2>/dev/null | sort > "$baseline_file"
    fi
    
    while true; do
        echo "Checking system state..."
        find / -type f -exec md5sum {} + 2>/dev/null | sort > "$current_state_file"
        
        diff "$baseline_file" "$current_state_file" > changes.txt
        
        if [ -s changes.txt ]; then
            echo "System changes detected!"
            mail -s "System Changes Alert" admin@example.com < changes.txt
        else
            echo "No changes detected."
        fi
        
        sleep 3600  # Check every hour
    done
}

monitor_system_changes
```

### 4.4 Automated Threat Intelligence Gathering
```bash
#!/bin/bash

gather_threat_intel() {
    local api_key="your_api_key_here"
    local indicators_file="indicators.txt"
    local results_file="threat_intel_results.json"
    
    while read -r indicator; do
        echo "Gathering intel for $indicator"
        curl -s -X GET "https://api.threatintelligence.com/v1/indicator/$indicator" \
             -H "Authorization: Bearer $api_key" >> "$results_file"
    done < "$indicators_file"
    
    echo "Threat intelligence gathering complete. Results in $results_file"
}

gather_threat_intel
```

### 4.5 Security Compliance Checker
```bash
#!/bin/bash

check_compliance() {
    local compliance_standard=$1
    local results_file="compliance_results.txt"
    
    echo "Checking compliance with $compliance_standard" > "$results_file"
    
    case $compliance_standard in
        "PCI-DSS")
            # Check firewall configuration
            iptables -L >> "$results_file"
            
            # Check for insecure services
            netstat -tuln | grep -E ':21|:23|:80' >> "$results_file"
            
            # Check password policies
            grep -E '^PASS_MAX_DAYS|^PASS_MIN_DAYS|^PASS_WARN_AGE' /etc/login.defs >> "$results_file"
            ;;
        "HIPAA")
            # Check encryption
            grep -i encrypt /etc/ssh/sshd_config >> "$results_file"
            
            # Check audit logging
            auditctl -l >> "$results_file"
            
            # Check access controls
            ls -l /etc/passwd /etc/shadow >> "$results_file"
            ;;
        *)
            echo "Unknown compliance standard: $compliance_standard" >> "$results_file"
            ;;
    esac
    
    echo "Compliance check complete. Results in $results_file"
}

check_compliance "PCI-DSS"
```

These scripts demonstrate the progression from basic Bash scripting to advanced cybersecurity applications. Remember to always test scripts in a safe environment and ensure you have the necessary permissions before running them, especially those that modify system configurations or access sensitive information.