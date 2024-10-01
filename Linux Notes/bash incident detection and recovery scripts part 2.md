Here’s an advanced [[Linux]] bash script that performs basic network reconnaissance and security checks. The script will:

- Perform port scanning using `nmap`.
- Check for open ports on a given target.
- Perform a basic vulnerability scan.
- Log the results for further analysis.

This script can be adapted and expanded based on specific needs.

### Advanced Bash Script for Network Reconnaissance and Security Checks

```bash
#!/bin/bash

# Advanced Bash Script for Network Reconnaissance

# Check if user is root
if [[ $EUID -ne 0 ]]; then
   echo "This script must be run as root." 
   exit 1
fi

# Define colors for better visibility in logs and terminal output
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color

# Function to check if required tools are installed
function check_dependencies() {
    echo -e "${GREEN}[*] Checking for required tools...${NC}"
    REQUIRED_TOOLS=("nmap" "curl" "openssl")
    for tool in "${REQUIRED_TOOLS[@]}"; do
        if ! command -v $tool &> /dev/null; then
            echo -e "${RED}[!] $tool is not installed. Install it to proceed.${NC}"
            exit 1
        fi
    done
    echo -e "${GREEN}[*] All tools are installed.${NC}"
}

# Function to perform port scanning
function port_scan() {
    target=$1
    echo -e "${GREEN}[*] Performing port scan on $target...${NC}"
    nmap -sS -Pn -T4 $target -oN nmap_scan_$target.txt
    echo -e "${GREEN}[*] Port scan completed. Results saved in nmap_scan_$target.txt.${NC}"
}

# Function to perform basic vulnerability scan (example: checking for SSL vulnerabilities)
function ssl_check() {
    domain=$1
    echo -e "${GREEN}[*] Checking SSL/TLS vulnerabilities on $domain...${NC}"
    sslscan --no-failed $domain > ssl_scan_$domain.txt
    echo -e "${GREEN}[*] SSL/TLS vulnerability check complete. Results saved in ssl_scan_$domain.txt.${NC}"
}

# Function to check if a specific port is open
function check_open_port() {
    target=$1
    port=$2
    echo -e "${GREEN}[*] Checking if port $port is open on $target...${NC}"
    if nc -zv $target $port &> /dev/null; then
        echo -e "${GREEN}[*] Port $port is open on $target.${NC}"
    else
        echo -e "${RED}[!] Port $port is closed on $target.${NC}"
    fi
}

# Function to perform HTTP header analysis
function http_headers() {
    url=$1
    echo -e "${GREEN}[*] Fetching HTTP headers for $url...${NC}"
    curl -I $url > http_headers_$url.txt
    echo -e "${GREEN}[*] HTTP headers saved in http_headers_$url.txt.${NC}"
}

# Function to check for basic website vulnerabilities
function basic_vuln_scan() {
    url=$1
    echo -e "${GREEN}[*] Performing basic vulnerability scan on $url...${NC}"
    curl -s $url | grep -i "X-Content-Type-Options" > /dev/null
    if [ $? -eq 0 ]; then
        echo -e "${GREEN}[*] X-Content-Type-Options header found.${NC}"
    else
        echo -e "${RED}[!] X-Content-Type-Options header not found. Possible MIME-type sniffing vulnerability.${NC}"
    fi

    curl -s $url | grep -i "X-Frame-Options" > /dev/null
    if [ $? -eq 0 ]; then
        echo -e "${GREEN}[*] X-Frame-Options header found.${NC}"
    else
        echo -e "${RED}[!] X-Frame-Options header not found. Possible Clickjacking vulnerability.${NC}"
    fi
}

# Main function
function main() {
    # Ensure dependencies are installed
    check_dependencies

    # Get the target from the user
    read -p "Enter the target domain or IP: " target
    read -p "Enter a specific port to check (leave blank to skip): " port
    read -p "Do you want to perform an SSL vulnerability scan (y/n)? " ssl_scan
    read -p "Do you want to fetch HTTP headers (y/n)? " http_headers_choice
    read -p "Do you want to perform a basic website vulnerability scan (y/n)? " vuln_scan

    # Perform port scan
    port_scan $target

    # Check a specific port if provided
    if [[ ! -z "$port" ]]; then
        check_open_port $target $port
    fi

    # Perform SSL check if the user agrees
    if [[ $ssl_scan == "y" || $ssl_scan == "Y" ]]; then
        ssl_check $target
    fi

    # Fetch HTTP headers if requested
    if [[ $http_headers_choice == "y" || $http_headers_choice == "Y" ]]; then
        http_headers $target
    fi

    # Perform basic vulnerability scan if requested
    if [[ $vuln_scan == "y" || $vuln_scan == "Y" ]]; then
        basic_vuln_scan $target
    fi
}

# Start the script
main
```

### Explanation of Key Functions:

1. **Port Scan (`nmap`)**:
   - Scans the target for open ports.
   - Results are saved in `nmap_scan_target.txt`.

2. **SSL Vulnerability Check**:
   - Uses `sslscan` to check SSL/TLS vulnerabilities on the given domain.

3. **Open Port Check**:
   - Uses `nc` (netcat) to check if a specific port is open.

4. **HTTP Header Analysis**:
   - Fetches the HTTP headers for a given URL using `curl`.
   - Saves the result in `http_headers_url.txt`.

5. **Basic Vulnerability Scan**:
   - Checks for specific headers like `X-Content-Type-Options` and `X-Frame-Options`, which can help mitigate MIME-type sniffing and clickjacking attacks.

### Requirements:
- `nmap`: For port scanning.
- `curl`: To fetch HTTP headers.
- `sslscan`: To check SSL/TLS vulnerabilities.
- `nc` (netcat): For checking open ports.

Make sure to run the script with root privileges to allow full functionality, especially for network scans (`nmap`). 

You can extend this script further based on your cybersecurity needs, such as adding more vulnerability checks, automating reporting, or integrating it with other security tools.