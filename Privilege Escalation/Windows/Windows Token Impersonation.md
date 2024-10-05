[[Windows Privilege Escalation]] 
**Token Impersonation** is a technique where an attacker gains access to a legitimate security token that belongs to another user or service, allowing the attacker to impersonate that user or service within a system. Tokens are used in authentication and authorization processes to validate a user's identity and permissions, especially in systems that use technologies like OAuth, Kerberos, or Microsoft Windows access tokens.

### **How Token Impersonation Works:**

1. **Token Generation:** A legitimate user or service is authenticated, and a token (which can be a session token, access token, refresh token, etc.) is generated to represent the user's session and permissions.
2. **Token Theft or Hijacking:** An attacker steals or gains access to the legitimate token. This can happen through various methods such as phishing, man-in-the-middle attacks, or exploiting vulnerabilities in applications or protocols.
3. **Token Replay or Usage:** The attacker uses the stolen token to impersonate the legitimate user or service, often bypassing the need for login credentials (like username and password).
4. **Privilege Escalation:** If the stolen token belongs to a highly privileged user (e.g., an admin), the attacker can escalate privileges and access sensitive resources or perform unauthorized actions.

---

### **Examples of Token Impersonation Attacks:**

#### **1. Pass-the-Token Attack (Windows Environment)**
In a Windows environment, access tokens are used for authentication. In a Pass-the-Token attack, an attacker captures and reuses a legitimate user's access token to impersonate them.

- **Steps:**
  - The attacker compromises a low-privileged user account.
  - They extract the user’s access token from memory using tools like **Mimikatz**.
  - The attacker uses the stolen token to impersonate the user or an admin without knowing the password, allowing lateral movement in the network.

- **Example:**
  If an attacker compromises a machine where a domain administrator has logged in, they can steal the domain admin’s access token and use it to gain administrative privileges across the network.

#### **2. OAuth Token Impersonation Attack**
OAuth is a common authorization protocol that uses access tokens. In an OAuth Token Impersonation attack, an attacker steals an OAuth token to access the victim’s account in a third-party service (e.g., Google, Facebook, GitHub).

- **Steps:**
  - The attacker compromises the OAuth flow, such as through a **phishing attack**.
  - They trick the user into authorizing the attacker’s app or site, which in turn issues a token.
  - The attacker uses this token to access resources that the victim has authorized.

- **Example:**
  An attacker gains an OAuth token from a user’s compromised application. Using that token, they can access the user’s cloud storage or email account without the need for further authentication.

#### **3. Kerberos Golden Ticket Attack**
In a Kerberos-based system (often used in Windows domains), an attacker with domain-level privileges can generate a "Golden Ticket" by impersonating the Ticket Granting Ticket (TGT), which can be used to access resources across the domain.

- **Steps:**
  - The attacker gains access to the domain controller and extracts the **krbtgt** account's hash.
  - They use tools like Mimikatz to create a forged TGT (Golden Ticket) for any user, including domain admins.
  - The attacker can now impersonate any user indefinitely, bypassing all authentication mechanisms.

- **Example:**
  The attacker forges a Golden Ticket and impersonates a domain administrator, gaining full control over the Active Directory and any associated services.

#### **4. JSON Web Token (JWT) Manipulation**
JWTs are used in web applications for authentication and authorization. In JWT Token Impersonation, the attacker manipulates the token or forges a token to bypass authentication.

- **Steps:**
  - An attacker identifies a vulnerability in token validation, such as weak signature algorithms or improper verification of the token's payload.
  - The attacker forges a JWT that impersonates a privileged user or modifies the claims in the token.
  - The attacker sends the malicious token to the web application, which incorrectly validates it, granting the attacker unauthorized access.

- **Example:**
  An attacker notices that the application is using **HMAC** instead of **RSA** for signing tokens. They create their own signed token, using the same secret key, and impersonate an admin user by setting the **“role”** claim to **“admin”**.

---

### **Mitigation Techniques:**

1. **Multi-Factor Authentication (MFA):** Use MFA to make it harder for attackers to gain access even if a token is compromised.
2. **Token Expiry:** Implement short-lived tokens to limit the damage of stolen tokens.
3. **Token Binding:** Ensure tokens are bound to specific devices or sessions so that they can’t be used in another context.
4. **Secure Token Storage:** Ensure tokens are stored securely (e.g., in secure HTTP-only cookies or secure vaults).
5. **Logging and Monitoring:** Track token usage and look for anomalies in token-related activity.
6. **Signature Validation:** Ensure proper token validation mechanisms are in place, especially for JWTs, OAuth, etc.

Token impersonation can be devastating if not mitigated, as it enables attackers to access resources and perform actions as legitimate users.