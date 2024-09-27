Privilege escalation is a technique that allows users to gain access to resources or privileges they aren't initially granted. This can lead to unauthorized access to sensitive data, system compromise, and potential further attacks on connected systems.
When there is a file misconfiguration, this can lead to unauthorize access to that sensitive. An example is /etc/shadow, which should not be accessible by any user but root.

***/etc/passwd*** - contains username and a place holder that (), that supposed to contain the user's password. Users can read usually this file.

***/etc/shadow*** -  shadow is a file which contains the password information for the system's accounts and optional aging information.
This file must not be readable by regular users if password security is to be maintained.

***unshadow*** - combines passwd and shadow files. The unshadow tool combines the passwd and shadow files so John (the Ripper) can use them.

