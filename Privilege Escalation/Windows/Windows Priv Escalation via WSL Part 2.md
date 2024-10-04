### [[Windows Privilege Escalation]] via Windows Subsystem for Linux (WSL)

In a Windows environment, **Windows Subsystem for Linux (WSL)** can sometimes be misconfigured or exploited, allowing for privilege escalation, especially if users with administrative privileges have enabled WSL without securing it properly.

Here's a step-by-step breakdown of how privilege escalation via WSL could work, along with an example. **Note:** This is for educational purposes only. Always ensure you're working within legal boundaries such as penetration testing agreements.

---

### Step 1: Verify WSL Installation

Check if the target machine has WSL installed.

#### Command:

```bash
wsl -l
```

This command lists all installed WSL distributions.

---

### Step 2: Gain Access to a Low-Privileged User Account

In this scenario, you have access to a low-privileged account on the Windows machine, either through phishing, credential stuffing, or a lateral movement within the network.

#### Example:

Let’s assume we have obtained a low-privileged user shell on the Windows machine.

---

### Step 3: Check for Administrative Users in the WSL Environment

Once inside the WSL environment, the next step is to check whether the Linux distribution in WSL runs any processes or has access to administrative-level privileges.

#### Example:

Let’s check the permissions of the current user:

```bash
id
```

If the `uid=0(root)` appears, it means you are running with root privileges inside WSL. This is common as many users configure WSL to run as root by default.

---

### Step 4: Abuse WSL Configuration to Escalate Privileges

WSL inherits the permissions of the Windows user who starts it. If the WSL instance is running with elevated (Administrator) privileges, we can exploit this to perform malicious actions in Windows.

#### Attack Vector:

Using the `root` access inside WSL, you can execute Windows commands that require administrative privileges. WSL has access to Windows file systems and processes, so executing a command from within WSL can be done as an Administrator.

For instance, you can manipulate system files or install malicious software.

---

### Step 5: Use PowerShell from WSL to Escalate Privileges

We can invoke PowerShell commands from within WSL to perform privilege escalation tasks.

#### Example:

Run the following command from inside WSL to execute PowerShell as an Administrator and add a new user to the Administrators group.

```bash
powershell.exe -c "New-LocalUser -Name hacker -Password (ConvertTo-SecureString 'P@ssw0rd!' -AsPlainText -Force); Add-LocalGroupMember -Group Administrators -Member hacker"
```

Explanation:
- `New-LocalUser`: Creates a new local user with the name `hacker`.
- `Add-LocalGroupMember`: Adds the new user `hacker` to the `Administrators` group.

---

### Step 6: Verify Privilege Escalation

After executing the command, log into the Windows machine with the new user and check whether it has administrative privileges.

#### Example:

Open a new Command Prompt or PowerShell and type:

```powershell
whoami /groups
```

This will list the groups that the user belongs to. If you see "Administrators", it means the privilege escalation was successful.

---

### Step 7: Clean Up (Optional)

If this was part of a penetration test or red team assessment, ensure that you clean up any malicious users or artifacts created during testing.

#### Example:

```bash
powershell.exe -c "Remove-LocalUser -Name hacker"
```

---

### Mitigations

1. **Limit Administrative Privileges:** Ensure WSL is not running with root by default and the Windows user is not an Administrator.
2. **Apply Least Privilege:** Users should only have the necessary permissions.
3. **Monitor for Suspicious Behavior:** Monitor for PowerShell or WSL execution that might be unusual in your environment.
4. **Disable WSL if not needed:** If WSL is not required, consider disabling it entirely.

---

### Summary:

1. **Check for WSL:** Determine if WSL is installed and accessible.
2. **Explore the WSL environment:** Identify user permissions and look for misconfigurations.
3. **Invoke PowerShell through WSL:** Leverage WSL to run PowerShell commands that escalate privileges.
4. **Confirm Privilege Escalation:** Ensure the new user is part of the Administrators group.

---

This method of privilege escalation highlights the potential risks if WSL is improperly configured or if a malicious actor gains access to a system with WSL installed. Proper hardening and monitoring of WSL is crucial to prevent this attack.