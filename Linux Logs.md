Logs in every digital device play an important role in understanding what happened. Similarly, logs in Linux are essential for monitoring and tracking system activities, detecting attacks, and identifying incident surfaces. The logs contain records of each event or activity on the system, which could be valuable when identifying and investigating security-related incidents.  

In the earlier task, we examined auth.log to check the user creation-related logs.  
Let's explore some common incidents to understand the importance of logs and how they can be examined for potential incident traits.

Important logs are covered below:  

**Syslog:**

- Location: `/var/log/syslog`
- This is useful for identifying system-wide events, errors, and warnings. Can provide insights into issues with system components or services.
- It contains general system messages, including kernel messages, system services, and application logs.
- This log file is useful for identifying system-wide events, errors, and warnings.
- It can provide insights into issues with system components or services.

![Shows syslog content](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/5e8dd9a4a45e18443162feab-1725847386528.png)  

**Messages:**

- Location: `/var/log/messages`
- Similar to `syslog`, this file includes system messages and kernel logs.
- Useful for diagnosing system issues and tracking system activity.
- Finding unusual entries related to hardware or kernel errors might signal an attempt to tamper with system components.
- For example, repeated kernel panic messages could indicate a denial-of-service attack targeting system stability.

**Authentication Logs:**

- Location: `/var/log/auth.log`
- This file logs authentication attempts, including successful and failed login attempts.
- It's an important log file for detecting unauthorized access attempts and brute-force attacks.
- For example, finding multiple failed login attempts from an unfamiliar IP address or unusual login times might indicate a brute-force attack or an attempt to gain unauthorized access.

![Shows auth.log content](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/5e8dd9a4a45e18443162feab-1725851831948.png)  

Some of the key examples of the events that can be classified as incidents are:

- Failed login attempts.
- Successful login attempt but at the odd time (After Office Hours or on weekends -> depending on the context of the company).
- Suspicious network communication.
- System errors.
- User account creation on the sensitive server.
- Outbound traffic is initiated from the web server.