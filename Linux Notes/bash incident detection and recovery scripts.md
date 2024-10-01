#!/bin/bash

# Advanced Cybersecurity Bash Scripts for Incident Response, Recovery, and Threat Detection

# 1. Automated Incident Response Script

incident_response() {
    local target_ip=$1
    local incident_dir="/var/log/incidents/$(date +%Y%m%d_%H%M%S)"
    
```
    mkdir -p "$incident_dir"
    
    # Collect system information
    ssh root@"$target_ip" "
        hostname > $incident_dir/hostname.txt
        date > $incident_dir/incident_time.txt
        uname -a > $incident_dir/uname.txt
        ifconfig > $incident_dir/network_config.txt
        ps aux > $incident_dir/running_processes.txt
        netstat -antup > $incident_dir/network_connections.txt
        last > $incident_dir/last_logins.txt
        grep -Ev '^#|^$' /etc/passwd > $incident_dir/passwd.txt
        grep -Ev '^#|^$' /etc/shadow > $incident_dir/shadow.txt
    "
    
    # Collect volatile data
    ssh root@"$target_ip" "
        dd if=/dev/mem of=$incident_dir/memory.dump bs=1M
        volatility -f $incident_dir/memory.dump imageinfo > $incident_dir/volatility_imageinfo.txt
        volatility -f $incident_dir/memory.dump --profile=LinuxCentOS7_3_10_0-1062x64 linux_pslist > $incident_dir/volatility_pslist.txt
        volatility -f $incident_dir/memory.dump --profile=LinuxCentOS7_3_10_0-1062x64 linux_netstat > $incident_dir/volatility_netstat.txt
    "
    
    # Collect logs
    ssh root@"$target_ip"
        tar czf $incident_dir/var_log.tar.gz /var/log
        journalctl -o json-pretty > $incident_dir/journalctl.json
    
    
    echo "Incident data collected and stored in $incident_dir"
}
```

# 2. Malware Analysis and Containment

```
analyze_and_contain_malware() {
    local suspicious_file=$1
    local quarantine_dir="/var/quarantine"
    
    mkdir -p "$quarantine_dir"
    
    # Static analysis
    file "$suspicious_file" > "$quarantine_dir/file_info.txt"
    md5sum "$suspicious_file" > "$quarantine_dir/md5_hash.txt"
    sha256sum "$suspicious_file" > "$quarantine_dir/sha256_hash.txt"
    strings "$suspicious_file" > "$quarantine_dir/strings_output.txt"
    
    # Check against VirusTotal (requires API key)
    vt_api_key="YOUR_VIRUSTOTAL_API_KEY"
    sha256=$(sha256sum "$suspicious_file" | cut -d' ' -f1)
    curl -s -X GET "https://www.virustotal.com/api/v3/files/$sha256" \
         -H "x-apikey: $vt_api_key" > "$quarantine_dir/virustotal_report.json"
    
    # Sandbox analysis (example using Cuckoo Sandbox)
    cuckoo submit "$suspicious_file"
    
    # Contain the file
    mv "$suspicious_file" "$quarantine_dir/"
    chattr +i "$quarantine_dir/$(basename "$suspicious_file")"
    
    echo "Malware analysis complete. File quarantined in $quarantine_dir"
}

```
# 3. Network-based Threat Detection

```
detect_network_threats() {
    local interface="eth0"
    local pcap_file="/tmp/capture.pcap"
    local alert_log="/var/log/network_threats.log"
    
    # Capture network traffic
    tcpdump -i "$interface" -w "$pcap_file" -G 3600 -W 24 &
    
    # Analyze traffic with Suricata
    suricata -c /etc/suricata/suricata.yaml -i "$interface" &
    
    # Monitor Suricata alerts
    tail -f /var/log/suricata/fast.log | while read line; do
        echo "$(date): $line" >> "$alert_log"
        
        # Check for critical alerts
        if echo "$line" | grep -q "CRITICAL"; then
            source_ip=$(echo "$line" | awk '{print $5}' | cut -d: -f1)
            # Block the IP
            iptables -A INPUT -s "$source_ip" -j DROP
            echo "$(date): Blocked $source_ip due to critical alert" >> "$alert_log"
        fi
    done
}

```
# 4. System Integrity Monitoring

```
monitor_system_integrity() {
    local baseline_file="/var/lib/aide/aide.db"
    local check_interval=3600  # 1 hour
    
    # Initialize AIDE database if it doesn't exist
    if [ ! -f "$baseline_file" ]; then
        aide --init
        mv /var/lib/aide/aide.db.new "$baseline_file"
    fi
    
    while true; do
        # Check system integrity
        aide --check > /tmp/aide_check.log 2>&1
        
        # If changes detected, alert and update baseline
        if grep -q "found differences between database and filesystem" /tmp/aide_check.log; then
            echo "System changes detected at $(date)" | mail -s "Integrity Alert" admin@example.com
            aide --update
            mv /var/lib/aide/aide.db.new "$baseline_file"
        fi
        
        sleep "$check_interval"
    done
}

```
# 5. Automated Recovery Script

```
system_recovery() {
    local backup_dir="/mnt/backups"
    local recovery_log="/var/log/recovery.log"
    
    echo "Starting system recovery at $(date)" > "$recovery_log"
    
    # Stop non-essential services
    systemctl stop apache2 mysql
    
    # Check and repair filesystem
    fsck -y /dev/sda1 >> "$recovery_log" 2>&1
    
    # Restore from latest backup
    latest_backup=$(ls -t "$backup_dir" | head -n1)
    tar xzf "$backup_dir/$latest_backup" -C / >> "$recovery_log" 2>&1
    
    # Update all packages
    apt update && apt upgrade -y >> "$recovery_log" 2>&1
    
    # Rebuild initramfs
    update-initramfs -u -k all >> "$recovery_log" 2>&1
    
    # Reset user passwords
    echo "root:$(openssl rand -base64 12)" | chpasswd
    
    # Restart essential services
    systemctl start apache2 mysql
    
    echo "System recovery completed at $(date)" >> "$recovery_log"
}

```
# Main execution
```
case "$1" in
    "incident_response")
        incident_response "$2"
        ;;
    "analyze_malware")
        analyze_and_contain_malware "$2"
        ;;
    "detect_threats")
        detect_network_threats
        ;;
    "monitor_integrity")
        monitor_system_integrity
        ;;
    "recover")
        system_recovery
        ;;
    *)
        echo "Usage: $0 {incident_response|analyze_malware|detect_threats|monitor_integrity|recover}"
        exit 1
        ;;
esac

exit 0
```