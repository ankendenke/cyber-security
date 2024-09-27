Let's pretend to be Bob, a blue teamer trying to examine various [[Linux Incident Surface]] to identify the footprints of the backdoor account that was created.

**Examining Logs**

One of the key places we could begin looking at would be the logs. All common logs can be found at the `/var/log/` location, as shown below:

Listing /var/log directory  

```shell-session
ubuntu@tryhackme:/home$ cd /var/log/
ubuntu@tryhackme:/var/log$ ls -al
total 3108
drwxrwxr-x  16 root              syslog             4096 Sep  5 00:00 .
drwxr-xr-x  14 root              root               4096 Feb 27  2022 ..
-rw-r--r--   1 root              root              35148 Aug 20 07:34 Xorg.0.log
-rw-r--r--   1 root              root             116188 Feb 16  2024 Xorg.0.log.old
-rw-r--r--   1 root              root                  0 Sep  1 00:00 alternatives.log
-rw-r--r--   1 root              root               8021 Aug 22 06:57 alternatives.log.1
-rw-r--r--   1 root              root               3001 Feb 16  2024 alternatives.log.2.gz
drwxr--r-x   3 root              root               4096 Feb 27  2022 amazon
-rw-r-----   1 root              adm                   0 Aug 20 07:34 apport.log
-rw-r-----   1 root              adm                 398 Feb 16  2024 apport.log.1
drwxr-xr-x   2 root              root               4096 Sep  5 06:52 apt
-rw-r-----   1 syslog            adm               46892 Sep  5 21:30 auth.log
-rw-r-----   1 syslog            adm               72850 Aug 31 23:30 auth.log.1
-rw-r-----   1 syslog            adm                3325 Aug 24 23:30 auth.log.2.gz
-rw-r-----   1 syslog            adm                9404 Aug 20 07:34 auth.log.3.gz
-rw-rw----   1 root              utmp                  0 Sep  1 00:00 btmp
-rw-rw----   1 root              utmp               3840 Aug 27 14:04 btmp.1
-rw-r-----   1 root              adm               44217 Aug 20 07:34 cloud-init-output.log
-rw-r-----   1 syslog            adm             1576538 Aug 20 07:34 cloud-init.log
drwxr-xr-x   2 root              root               4096 Sep  5 00:00 cups
drwxr-xr-x   2 root              root               4096 Oct  7  2020 dist-upgrade
------------------------------------------
```

**Examining auth.log**

Let's use the following command to search for all user account creation activities in the auth.log, as shown below:  
**Command:** `cat auth.log | grep useradd`  

Examining auth.log  

```shell-session
ubuntu@tryhackme:/var/log$ sudo su
root@tryhackme:/var/log# cat auth.log | grep useradd
Sep  5 21:18:19 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home ; USER=root ; COMMAND=/usr/sbin/useradd attacker -G sudo
Sep  5 21:18:19 tryhackme useradd[184928]: new group: name=attacker, GID=1001
Sep  5 21:18:19 tryhackme useradd[184928]: new user: name=attacker, UID=1001, GID=1001, home=/home/attacker, shell=/bin/sh, from=/dev/pts/0
Sep  5 21:18:45 tryhackme sudo:   ubuntu : TTY=pts/0 ; PWD=/home ; USER=root ; COMMAND=/usr/sbin/useradd attacker -G sudo
```

  
If we look at the output, we can see various log entries associated with the user account creation activity.  

**Examining /etc/passwd File**  

Another configuration file called passwd also contains information about the users created either by default or by users, as shown below:

**Command:** `cat /etc/passwd`  

Examining /etc/passwd  

```shell-session
root@tryhackme:/var/log# cat /etc/passwd
---
----------
kernoops:x:113:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
lightdm:x:114:121:Light Display Manager:/var/lib/lightdm:/bin/false
whoopsie:x:115:123::/nonexistent:/bin/false
dnsmasq:x:116:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
avahi-autoipd:x:117:124:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
usbmux:x:118:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:119:125:RealtimeKit,,,:/proc:/usr/sbin/nologin----------------------------
avahi:x:120:126:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
fwupd-refresh:x:130:136:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
attacker:x:1001:1001::/home/attacker:/bin/sh
```

  
In the output, we can see all the accounts, including the one we just created. Some of the information this file contains are:

- Username.
- The password placeholder is represented by x or *, indicating that the password is stored in the/etc/shadow file.
- User ID assigned to the user
- Group ID assigned to the user.
- User's home directory.
- Path to user's default shell.
