[[Windows Privilege Escalation]]
The **Potato attack** is a family of privilege escalation vulnerabilities and techniques that exploit Windows' token-based authentication mechanisms to elevate privileges. The most famous of these is **Juicy Potato**, but there are also others like **Rogue Potato** and **Hot Potato**. These attacks take advantage of how Windows handles token impersonation and the way services interact with each other using COM/DCOM (Component Object Model/Distributed COM) and other Windows components.

Here's an elaboration on each of these attacks:

---

### **1. Hot Potato Attack (aka "Rotten Potato")**

The **Hot Potato Attack** is a Windows privilege escalation attack that leverages weaknesses in Windows’ **NTLM authentication** and **local privilege escalation**.

#### **Key Components of the Attack:**

- **NTLM Relay Attack:** The attacker intercepts and relays NTLM authentication requests to escalate privileges.
- **Windows Token Impersonation:** The attack abuses the token impersonation feature in Windows to impersonate a more privileged user (usually SYSTEM).

#### **Steps Involved:**

1. **Network Capture with WPAD (Web Proxy Auto-Discovery):**
   - The attacker sets up a rogue WPAD proxy server on the victim’s network.
   - When the Windows service attempts to make an HTTP request, the attacker intercepts the NTLM challenge/response authentication traffic.

2. **NTLM Relay:**
   - The attacker relays the captured NTLM authentication to another service on the same machine, such as the SMB (Server Message Block) service.
   - This forces a high-privileged service (like SYSTEM or Administrator) to authenticate to the attacker-controlled service.

3. **Impersonating SYSTEM:**
   - Once the NTLM token is relayed, the attacker can leverage the token to impersonate SYSTEM privileges, allowing them to execute commands with elevated privileges.

#### **Use Cases:**
- Hot Potato is commonly used in environments where there are misconfigurations that allow NTLM authentication to be relayed between services. It is often useful in post-exploitation scenarios where the attacker already has a foothold in the system with lower privileges.

---

### **2. Juicy Potato Attack**

**Juicy Potato** is a privilege escalation technique that targets misconfigured Windows systems, particularly those that run services with **Service Account Tokens** like **Local Service**, **Network Service**, or **Administrator**. It exploits a flaw in how Windows handles COM and DCOM interfaces.

#### **Key Concepts:**

- **COM/DCOM (Component Object Model):** Windows uses COM/DCOM for inter-process communication (IPC). Some of these processes run under SYSTEM privileges.
- **Token Impersonation:** Services that run under service accounts (e.g., Local Service) have impersonation tokens that can be abused if not handled properly.

#### **Steps Involved:**

1. **Abusing DCOM to Get an Impersonation Token:**
   - Juicy Potato exploits a weakness in the Windows **DCOM** service, where it can request a privileged token (e.g., SYSTEM token) when running a service under Local Service or Network Service.
   
2. **Trigger COM Activation:**
   - The attacker uses Juicy Potato to trigger the activation of a **DCOM server** that is registered to run with elevated privileges. The attacker then tricks the system into giving them a SYSTEM-level token.

3. **Impersonating SYSTEM:**
   - The attacker impersonates the SYSTEM token that was obtained through the DCOM activation and executes commands as SYSTEM.

#### **Use Cases:**
- Juicy Potato is especially useful in scenarios where the attacker has access to a low-privileged service account (Local Service or Network Service) but wants to escalate to SYSTEM.

---

### **3. Rogue Potato Attack**

**Rogue Potato** is an evolution of Juicy Potato, created in response to mitigations and patches that affected the original technique. Microsoft introduced **RPC Filters** and other defenses that made Juicy Potato unreliable in newer Windows versions (e.g., Windows 10 and Server 2019).

#### **Key Concepts:**

- Like Juicy Potato, Rogue Potato also abuses the **COM/DCOM architecture** and **token impersonation**.
- Rogue Potato bypasses the restrictions Microsoft added to prevent token stealing using **RPC filters** and new restrictions introduced in Windows 10/Server 2019.

#### **Steps Involved:**

1. **Exploiting the COM System:**
   - Rogue Potato establishes a COM connection to a privileged service and attempts to impersonate a SYSTEM token, but it bypasses the mitigations (e.g., the new RPC filters).

2. **Manipulating the TCP/IP Stack:**
   - Rogue Potato abuses the **TCP/IP stack** to relay authentication requests and responses to different processes on the system to get a SYSTEM token.

3. **Token Impersonation:**
   - Once the SYSTEM token is captured, the attacker impersonates SYSTEM and executes commands with elevated privileges.

#### **Use Cases:**
- Rogue Potato is useful in situations where Juicy Potato no longer works due to Microsoft’s updates and mitigations.

---

### **4. Sweet Potato (Local System Escalation)**

**Sweet Potato** is a further evolution of these techniques, designed specifically for scenarios where **Local System** privilege escalation is needed. It works similarly to Juicy Potato and Rogue Potato but is more reliable on modern versions of Windows.

#### **Steps Involved:**

1. **Service Token Misuse:**
   - Sweet Potato targets services running under **LocalSystem** and uses DCOM and NTLM relay techniques to get elevated privileges.

2. **Privilege Escalation:**
   - The attacker captures a token for LocalSystem, then impersonates it to escalate privileges to SYSTEM.

---

### **Mitigations Against Potato Attacks:**

1. **Disable NTLM (or use it securely):**
   - Use more secure authentication protocols like **Kerberos** where possible.
   - Disable NTLM where it isn’t needed.

2. **Token Filtering:**
   - Ensure that **service account tokens** (like Local Service and Network Service) are properly configured with limited privileges.
   - Microsoft introduced **RPC filters** to prevent unauthorized COM/DCOM activations.

3. **Enable Windows Defender Credential Guard:**
   - This feature can prevent certain types of credential and token theft attacks, including some of the Potato-based techniques.

4. **Patch Systems:**
   - Keep systems up to date with security patches that address vulnerabilities in COM/DCOM and token impersonation.

---

### **Summary:**

Potato attacks like **Hot Potato**, **Juicy Potato**, **Rogue Potato**, and **Sweet Potato** are sophisticated privilege escalation techniques that exploit how Windows handles service account tokens and COM/DCOM processes. They all rely on **token impersonation**, which allows an attacker to elevate privileges to SYSTEM or Administrator. Each attack has evolved to bypass Microsoft’s security mitigations, with newer versions like Rogue Potato and Sweet Potato being more effective on modern Windows versions. 

These attacks are commonly used in **post-exploitation** scenarios, where an attacker has already compromised a system with low privileges and seeks to escalate their access to perform more critical operations.