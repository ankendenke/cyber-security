[[Linux]] The second-generation onion router

Start
```
sudo systemctl start tor
```
# Tor Guide for Security Researchers and Red Teamers

## 1. Introduction to Tor
- Tor (The Onion Router) is a network designed for anonymous communication
- Primary uses in security research:
  - OSINT investigations
  - Vulnerability assessment
  - Network security testing
  - Threat intelligence gathering

## 2. Setting Up Your Research Environment

### 2.1 Basic Setup
1. Download Tor Browser Bundle from the official website (torproject.org)
2. Consider using Tails OS or Whonix for enhanced security
3. Set up a dedicated research machine separate from personal use

### 2.2 Advanced Configuration
- Use bridges if needed
- Configure security settings in torrc:
  ```
  StrictNodes 1
  EntryNodes {countrycode}
  ExitNodes {countrycode}
  ```

## 3. Security Researcher Tools and Techniques

### 3.1 OSINT Tools for Tor
- OnionScan: Analyze onion services
- Maltego with Tor proxy configuration
- ExifTool through Tor for metadata analysis
- Nipe for system-wide Tor routing

### 3.2 Network Analysis
- Setting up Tor relay for network analysis
- Using metrics.torproject.org for network insights
- Analyzing Tor circuit creation
- Understanding guard nodes and exit policies

## 4. Red Team Operations

### 4.1 Operational Security
- Compartmentalization strategies
- Managing multiple Tor instances
- Circuit isolation techniques
- Identity separation practices

### 4.2 Common Pitfalls to Avoid
- Browser fingerprinting risks
- Time correlation attacks
- Exit node monitoring
- Operational mistakes that can deanonymize

## 5. Advanced Topics

### 5.1 Hidden Services
- Setting up and securing .onion services
- Hidden service authentication
- Load balancing and high availability
- Security considerations for hidden services

### 5.2 Traffic Analysis
- Understanding traffic patterns
- Detecting Tor traffic
- Analyzing Tor consensus data
- Exit node selection strategies

## 6. Best Practices

### 6.1 Documentation
- Maintaining detailed operation logs
- Recording methodology
- Documenting findings securely
- Report writing considerations

### 6.2 Legal and Ethical Considerations
- Obtaining proper authorization
- Understanding jurisdictional issues
- Ethical guidelines for testing
- Data handling and privacy concerns

## 7. Defensive Considerations

### 7.1 Detection and Monitoring
- Identifying Tor traffic in your network
- Setting up Tor exit node lists
- Implementing Tor network policies
- Monitoring for abuse

### 7.2 Incident Response
- Handling Tor-related incidents
- Evidence collection
- Attribution challenges
- Response strategies

## 8. Resources and Further Learning

### 8.1 Technical Documentation
- Tor specifications and protocols
- Research papers on Tor security
- Tools documentation
- Community resources

### 8.2 Training and Development
- Recommended learning paths
- Practice environments
- Certification considerations
- Community engagement opportunities