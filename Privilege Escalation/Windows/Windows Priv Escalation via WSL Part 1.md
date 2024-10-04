[[Windows Privilege Escalation]]  via WSL (Windows Subsystem for Linux) can occur when improper permissions or system misconfigurations are leveraged to gain elevated privileges. Let’s walk through a typical scenario of using WSL to escalate privileges from a low-privileged user account to SYSTEM.

### Prerequisites
1. **Windows 10/11 with WSL enabled**: Ensure WSL is enabled and running.
2. **Low-privileged access**: Start with a user account that has limited privileges on the system.
3. **Administrative tools**: You'll need some tools like PowerShell and a Linux distribution installed in WSL.

### Scenario: Privilege Escalation via WSL
1. **Check Privileges on WSL**:  
   As a regular user, check your current privileges on WSL and whether you can invoke administrative commands.

    Open a WSL terminal (e.g., Ubuntu) and run:
    ```bash
    id
    ```
    This will show your Linux UID (user ID) and GID (group ID). Typically, it should be a non-privileged user.

2. **Locate SUID Files (on Linux side)**:  
   SUID (Set User ID) files are binaries that run with the privileges of the file owner. First, check if there are any misconfigured SUID files within WSL that could be exploited.

    Run:
    ```bash
    find / -perm -u=s -type f 2>/dev/null
    ```

    If there are binaries owned by root but executable by users, they might be exploitable. However, in many modern systems, the Linux side of WSL will be more secure, so this step may not yield results.

3. **Abusing `wsl.exe` to Gain SYSTEM Access (on Windows side)**:  
   Now, the more critical escalation vector is on the Windows side. If you have limited user access but have WSL installed, there is a potential for escalation using `wsl.exe`.

   As a regular user, check if you can start WSL with administrative privileges:
   ```bash
   wsl.exe -u root
   ```

   If it opens a root shell, the user can potentially use the full capabilities of the root account. However, in a more secured system, this won't work because the user doesn't have sufficient privileges. In such a case, you can attempt to elevate privileges through other Windows misconfigurations.

4. **Leveraging Token Manipulation**:  
   Windows stores tokens for running processes, and with WSL, processes can sometimes inherit SYSTEM-level tokens if not properly isolated. Here, the focus is to steal a token or create a malicious one.

   Use **Impersonation Token Tools** like **Mimikatz** (or PowerShell for a simpler method) to manipulate tokens.

   Run the following PowerShell commands to view and impersonate tokens:
   ```powershell
   whoami /groups
   ```

   If a privileged group appears, such as `Administrators`, SYSTEM tokens might be accessible.

5. **Gaining SYSTEM Access via Process Injection**:  
   Suppose you find a SYSTEM process running that has a vulnerable service. You can inject code into this process to gain SYSTEM privileges.

   To enumerate processes running as SYSTEM:
   ```powershell
   Get-Process | Where-Object { $_.Name -eq "services" }
   ```

   If you identify a vulnerable service, use a tool like **Process Hacker** to inject into it, gaining SYSTEM access.

6. **Persistence and Backdoor**:  
   After achieving SYSTEM privileges, you can create persistence by adding a new admin user or altering system services.

   Add a new admin user:
   ```powershell
   net user hacker P@ssword123 /add
   net localgroup administrators hacker /add
   ```

   Alternatively, you can create a backdoor by modifying the registry or scheduled tasks.

7. **Cleanup**:  
   Once you’ve escalated your privileges, make sure to clean up to avoid detection. Remove logs or artifacts from the system that may indicate your activity.

---

### Concrete Example of Exploiting a Vulnerable Service

1. **Identify a service that interacts with WSL**: A real-world vulnerable service may interact with WSL binaries. For example, some software (antivirus, backup tools, etc.) could execute commands through WSL.

2. **Exploit an Injection Flaw**: If you find that this service is running with SYSTEM privileges but executes a user-supplied command via WSL, you can replace the executable or command to run your code with SYSTEM privileges.

---

### Key Takeaways:
- **WSL** is a useful tool for attackers to move laterally in Windows environments due to its ability to interact with both Windows and Linux systems.
- **WSL.exe** can be abused to launch commands with elevated privileges if improperly configured.
- **Token manipulation** or **injection** are common techniques to gain SYSTEM privileges from WSL.


THM box: Secnote
