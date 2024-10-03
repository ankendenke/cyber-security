***What's a stake***
[[Linux Privilege Escalation]] is ==a technique that allows users to gain elevated privileges or access to restricted resources==. This can be done by exploiting a weakness in a system or application, ==such as a password stored in plain text==.

The *history* command is a useful tool to begin with. One can also look for ***==.bash_history ==file in the user's directory.***

Linux users may store their passwords in plain text; if these files are not properly secured, we may access the user's account. **Once we locate a password, we can use it to escalate our privileges by logging into a higher-privileged account or using it with sudo to run commands with elevated privileges**.

```
history | grep pass
or
linpeas
or
find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;
or
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
```

Source: https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/linux-privilege-escalation/#looting-for-passwords

Also:
Look inside hidden configuration files, passwords may be used to setup services like, databases, daemons, etc...