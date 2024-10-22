As a security researcher, common vulnerabilities I often encounter fall into several key categories. These vulnerabilities can affect different layers of the IT stack, from applications and operating systems to networks and hardware. Below are some of the most frequent ones:

### 1. **Injection Attacks**
   - **SQL Injection**: Attackers manipulate queries sent to a database by injecting malicious SQL code into input fields (e.g., login forms, search bars). This can lead to unauthorized access to databases.
   - **Command Injection**: Attackers inject system commands into an application’s input fields, which are then executed by the server.
   - **Cross-Site Scripting (XSS)**: This allows attackers to inject malicious scripts into web pages viewed by other users, often used for stealing cookies, session tokens, or sensitive information.

### 2. **Authentication and Session Management Flaws**
   - **Weak Passwords/Password Reuse**: Poor password policies or allowing weak passwords leads to easy compromise.
   - **Session Hijacking**: Attacker gains access to a user’s session (e.g., by stealing session cookies) and impersonates the user.
   - **Credential Stuffing**: Automated injection of breached username-password pairs to gain unauthorized access.
   - **Broken Authentication**: Weaknesses in session or token management, such as improper session expiration or predictable session tokens.

### 3. **Broken Access Control**
   - **Privilege Escalation**: Attackers gain higher levels of access (e.g., user to admin) through improper permission controls.
   - **Insecure Direct Object References (IDOR)**: Direct access to objects (e.g., files, database records) based on user-supplied input without proper authorization checks.
   - **Cross-Site Request Forgery (CSRF)**: Exploits a user’s session to perform unauthorized actions on their behalf by tricking them into submitting a malicious request.

### 4. **Security Misconfiguration**
   - **Unpatched Vulnerabilities**: Software or hardware that is outdated or not updated regularly creates security holes.
   - **Exposed Admin Interfaces**: Lack of proper access restrictions on admin or back-end interfaces.
   - **Default Credentials**: Default passwords or settings left in place after deployment, making it easy for attackers to access.

### 5. **Insecure Cryptographic Storage**
   - **Weak Encryption**: Use of outdated or insecure cryptographic algorithms (e.g., MD5, SHA1) that can be broken by attackers.
   - **Improper Key Management**: Keys stored in plaintext, hard-coded in applications, or improperly rotated.
   - **Insufficient Data Encryption**: Sensitive data like passwords or personal information stored without encryption.

### 6. **Vulnerabilities in Third-Party Libraries and Dependencies**
   - **Dependency Confusion**: Attackers upload malicious packages that are mistakenly fetched by organizations relying on open-source package managers.
   - **Outdated Libraries**: Applications using third-party libraries or frameworks with known vulnerabilities.
   - **Supply Chain Attacks**: Compromise in the software supply chain through malicious dependencies or packages.

### 7. **Cross-Site Scripting (XSS)**
   - **Stored XSS**: Malicious scripts are permanently stored on a target server (e.g., in a database) and served to all users.
   - **Reflected XSS**: The malicious script is reflected off a web application to the victim's browser, often via a URL or form.
   - **DOM-based XSS**: The vulnerability exists in the client-side code (JavaScript), allowing an attacker to inject a script into the page's DOM.

### 8. **Insecure APIs**
   - **Improper Rate Limiting**: Lack of request throttling allows attackers to brute-force API calls or overload the system.
   - **Unprotected Endpoints**: APIs that lack proper authentication or authorization controls, leaving sensitive data exposed.
   - **Excessive Data Exposure**: APIs returning more data than needed, which can be leveraged by attackers.

### 9. **Buffer Overflows**
   - Occurs when a program writes more data to a block of memory (buffer) than it is intended to hold, potentially allowing attackers to execute arbitrary code or crash the system.

### 10. **Insufficient Logging and Monitoring**
   - Lack of proper logging or monitoring can make it difficult to detect and respond to attacks. This leads to delayed incident response, allowing attackers to go unnoticed.

### 11. **Insufficient Transport Layer Security**
   - **Unencrypted Traffic**: Sensitive data transmitted over HTTP or other unencrypted channels instead of HTTPS.
   - **Weak TLS Configurations**: Outdated or weak cryptographic protocols in use (e.g., SSLv3, TLS 1.0), exposing data to interception.

### 12. **Mobile Security Issues**
   - **Insecure Data Storage**: Sensitive data stored in insecure locations on a mobile device (e.g., without encryption).
   - **Reverse Engineering**: Mobile applications can be decompiled and analyzed, revealing sensitive data or API keys.
   - **Unprotected Communication Channels**: Data transmitted by mobile apps without proper encryption or over insecure networks.

### 13. **Denial of Service (DoS) and Distributed Denial of Service (DDoS)**
   - Attackers overwhelm the target system with traffic or resource-intensive requests, causing disruption or making the system unavailable.

### 14. **Weak Physical Security**
   - **Physical Access**: Insufficient physical security controls that allow attackers to access servers, network devices, or sensitive equipment.
   - **USB/Removable Media**: Insecure policies around the use of removable media can lead to malware introduction or data theft.

### 15. **Hardware/IoT Vulnerabilities**
   - **Insecure Firmware**: IoT devices with outdated or insecure firmware may be exploited for remote access or to create botnets.
   - **Side-Channel Attacks**: Exploiting physical hardware properties (e.g., power consumption, electromagnetic leaks) to extract sensitive information.

### 16. **Insufficient Cloud Security**
   - **Misconfigured Cloud Services**: Open S3 buckets, exposed cloud storage, or improperly secured virtual machines.
   - **Identity and Access Management (IAM) Misconfigurations**: Overly permissive IAM roles and policies can lead to privilege abuse.
   - **Container Vulnerabilities**: Issues like untrusted images, misconfigured Kubernetes, or Docker containers.

Each of these vulnerabilities can be exploited by attackers to compromise confidentiality, integrity, or availability of systems and data. As a security researcher, it's critical to identify, report, and sometimes help mitigate these issues before they can be leveraged in real-world attacks.