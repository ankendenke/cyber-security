### Privilege escalation
Privilege escalation is a technique used by hacker (or attacker) to gain unauthorized administrative right to a computer or network resources. Therefore allowing the attacker to do more damage.

Privilege Escalation refers to the process of exploiting misconfigurations, known vulnerabilities and unintented bugs in order to gain higher privileges on the target host. The final objective of this process is to gain the highest level of privileges on a target machine, achieving full compromise of that target.

Attackers exploit weaknesses in an operating system or application, such as bugs, configuration flaws, or poor application design, to steal administrative rights.

Depending on the privileges they gain, hackers can use them to access protected data and do whatever they want on the system.

There are 2 types on privilege escalation:
- Vertical: also known as privilege elevation, involves moving from a lower level of access to a higher one. For example, an attacker might use stolen credentials to access a host with regular privileges within a company's network, then identify a file server with sensitive data that multiple users can access. The attacker could then modify files within the shared file system to inject malicious code or replace critical configuration files.
- Horizontal:  when a user gains the access rights of another user who has the same access level as he or she does. Therefore the attacker may have access to sensitive data, or unauthorized operation otherwise not allowed to him.
![[Pasted image 20240730100443.png]]
Source: https://delinea.com/blog/linux-privilege-escalation (for the image only)
#### Protecting Against Privilege Escalation

There are many vulnerabilities that can lead to privilege escalation. Some of the most common are [[Cross-site scripting]], improper cookie handling, and [[Weak passwords]], [[Cross-site scripting]] and improper cookie handling can be protected against programmatically. [[Weak passwords]] require end-user education and the setting of password requirements. You can set requirements for password complexity and password age limits. There are two other widely used methods of preventing privilege escalation: they are the [[Principle of Least Privilege]] and the [[Separation of privileges]].

In conclusion: Privilege escalation is using a vulnerability to gain privileges other than what was originally intended for the user.

Practical [[Linux Privilege Escalation]]  steps
Practical [[Windows Escalation]] steps
