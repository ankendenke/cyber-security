
### **Beginner Level: Basic Scan Setup**

#### 1. **Login to Nessus**

- Open your browser and navigate to `https://localhost:8834`.
- Log in with your credentials.
- **What you'll see:** A dashboard with options like “New Scan” and “Settings.”

#### 2. **Create a New Scan**

- Click **“New Scan”** on the dashboard.
- Select **“Basic Network Scan”**.
    - This template is for general network vulnerability scanning.
- **What you'll see:** A configuration screen where you input scan details.

#### 3. **Configure the Scan**

- Enter a **name** for the scan, e.g., “Office Network Scan.”
- In **Targets**, add the IP addresses or ranges to scan.
    - Example: `192.168.1.1-192.168.1.254`.
- Save the scan by clicking **“Save”**.
- **What you'll see:** The scan is listed under “My Scans.”

#### 4. **Run the Scan**

- Click the play button next to your scan.
- Nessus will start scanning the targets.
- **What you'll see:** A progress bar showing the scan status.

#### 5. **Review the Results**

- After the scan completes, click the scan name to view results.
    - Results are categorized into severity levels: Critical, High, Medium, Low, and Info.
    - Click on individual vulnerabilities to see details, affected systems, and remediation steps.
- **What you'll see:** A detailed report with affected systems, CVSS scores, and recommendations.

---

### **Intermediate Level: Credentialed Scans**

#### 1. **Configure a Credentialed Scan**

- When creating a new scan, navigate to the **“Credentials”** tab in the configuration screen.
- Add credentials for SSH (Linux) or RDP (Windows).
    - For SSH: Enter username, private key, or password.
    - For Windows: Enter domain, username, and password.
- Save and run the scan.

#### 2. **Analyze Advanced Results**

- Credentialed scans provide deeper insights, such as:
    - Missing patches.
    - Misconfigured services.
    - Weak passwords.

**Expected Output:**

- A more comprehensive list of vulnerabilities, with system-level insights that are not visible in non-credentialed scans.

---

### **Expert Level: Using the Nessus API**

#### 1. **Enable API Access**

- Log into the Nessus web interface.
- Navigate to **Settings > Advanced**.
- Ensure **API Access** is enabled.

#### 2. **Access API Documentation**

- Visit `https://<nessus-ip>:8834/api`.

#### 3. **Automate a Scan (Example Using Python)**

Install Python’s requests library:

```bash
pip install requests
```

Example Script:

```python
import requests

# Nessus credentials
nessus_url = "https://localhost:8834"
username = "your_username"
password = "your_password"

# Login to Nessus
response = requests.post(
    f"{nessus_url}/session",
    json={"username": username, "password": password},
    verify=False
)
token = response.json()['token']

# Create a scan
headers = {"X-Cookie": f"token={token}"}
scan_data = {
    "uuid": "template_uuid",  # Get this from API or Nessus web
    "settings": {
        "name": "Automated Scan",
        "enabled": True,
        "text_targets": "192.168.1.1-192.168.1.254"
    }
}
scan = requests.post(f"{nessus_url}/scans", json=scan_data, headers=headers, verify=False)
print("Scan Created:", scan.json())
```

**What you'll see:** Output in your terminal confirming scan creation and further actions.