![[Pasted image 20240730103941.png]]
Source: https://delinea.com/blog/linux-privilege-escalation (image)

Some of the most common privileged accounts on Linux systems that attackers go after include:

- The King of Linux “root”
- The Secret Keys of Linux “the Private SSH key”
- The challenging and scary “sudoers users and setuid/setgid”
- The forgotten “System Adm Accounts”
- The help me “Emergency Accounts”
- The hidden and forever “Service Accounts such as www-data”
- The elevated “Dev Accounts”
- The silent but deadly “Privileged Data User Accounts”

Let's follow the steps on hacking:
#### Pentest 5 Stages
- Reconnaissance
- Scanning & Enumeration
- Exploitation
- Maintain Access
- Cover up tracks
For this topic's purpose we're interested in stages from 1 to 3
##### Recon
###### System Enumeration
Some useful command, once log into the target machine:
***hostname*** - show or set the system's host name
***uname*** -a - show all system information
***cat /proc/version*** - display the Linux OS version. 
***cat /etc/issue*** - display the Linux OS version
***lscpu*** - display information about the CPU architecture
***ps -aux*** - check the running services: look for web services, cron, file services look for vulnerabilities
In this phase we're looking for vulnerabilities from the kernel, to an individual services that might have some vulnerabilities that we can exploit.
###### User Enumeration
***whoami*** - print effective user name
***id*** - print real and effective user and group IDs
***sudo -l*** - list the privileges for the invoking user
***cat /etc/passwd*** - display the users on the system, unfortunately the password aren't stored here anymore
```
example: to select all the users on the system:
┌──(medtraore㉿medtraore-msi)-[~]
└─$ cat /etc/passwd | cut -d : -f 1
root
daemon
bin
sys
.
.
.
avahi
inetsim
_gvm
geoclue
polkitd
dradis
medtraore
debian-tor
john

```
***cat /etc/shadow*** - check which sensitive file we can access to
***cat /etc/group*** -  check which groups users belong to
###### Network Enumeration
The goal is to understand what is around this computer, what ports are open and listening to what services. Therefore what vuln we can exploit just by looking around the services and interfaces.
***ifconfig*** - configure a network interface
***ip -a*** - information about the network
***route*** - show / manipulate the ip routing table
```
Example
┌──(medtraore㉿medtraore-msi)-[~]
└─$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         medtraore-msi.m 0.0.0.0         UG    0      0        0 eth0
10.9.0.0        0.0.0.0         255.255.0.0     U     0      0        0 tun0
10.10.0.0       10.9.0.1        255.255.0.0     UG    1000   0        0 tun0
172.17.192.0    0.0.0.0         255.255.240.0   U     0      0        0 eth0
```
**ip neigh** - show the arp table 
```
┌──(root㉿medtraore-msi)-[~]
└─# ip neigh
172.17.192.1 dev eth0 lladdr 00:15:5d:51:f8:75 STALE
```
***netstat***  -  Print  network  connections, routing tables, interface statistics, masquerade
       connections, and multicast memberships
       This will check what ports are open and such
###### Password Hunting
Quick and dirty ways to look for password as some hanging fruit:
```
┌──(medtraore㉿medtraore-msi)-[~]
└─$grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null
```
```
medtraore㉿medtraore-msi-[~] locate password | more
```
```
medtraore㉿medtraore-msi-[~] find / -name id_rsa 2> /dev/null
```
##### Exploring Automated Tools
***Linpeas.sh*** - Automatically search the box for users and password for privilege escalation. On kali Linux, you can install it using the command below:
```
sudo apt install peass
```
***linEnum*** - This is an awesome Linux enumeration script. It’s run on the target host and searches for many of the common privilege escalation methods or misconfigurations.

Some of the enumeration information collected includes:

Kernel and distribution release details

- System information
- User information
- Privileged access
- Environmental information 

***Linux Exploit Suggester 2*** - This next-generation exploit suggester is based on Linux_Exploit_Suggester.

Key improvements include:

- More exploits!
- Option to download exploit code directly from Exploit DB
- Accurate wildcard matching. This expands the scope of searchable exploits.
- Output colorization for easy viewing.
- And more to come!

This script is extremely useful for quickly finding privilege escalation vulnerabilities both in on-site and exam environments.
https://github.com/jondonas/linux-exploit-suggester-2

***Linuxprivchecker.py*** - This script is intended to be executed locally on a Linux box to enumerate basic system info and search for common privilege escalation vectors such as world writable files, misconfigurations, clear-text passwords and applicable exploits.
https://github.com/sleventyeleven/linuxprivchecker

Let's go through some common exploitations using these tools

1- [[Kernel Exploitation]]
A kernel exploit is ==a cybersecurity threat that uses vulnerabilities in a computer's operating system (OS) kernel to gain unauthorized access to protected areas==. The kernel is a core program that controls many aspects of the system, including preventing conflicts between processes.

2- [[Escalation via Stored Passwords]]
A cyber security threat that uses passwords stored on user's computer, on captured on the history command.

3- [[Escalation via Weak File Permissions]]
Privilege escalation is a technique that allows users to gain access to resources or privileges they aren't initially granted. This can lead to unauthorized access to sensitive data, system compromise, and potential further attacks on connected systems.
When there is a file misconfiguration, this can lead to unauthorize access to that sensitive file. An example is /etc/shadow, which should not be accessible by any user but root.

3- [[Escalation via SSH Keys]]
Secure Shell (SSH) is a cryptographic network protocol which allows users to securely perform a number of network services, such as remote authentication or file transfer, over an unsecured network. SSH keys provide a more secure way of logging into a server through SSH than via a password authentication.

If improperly configured, SSH keys could allow an attacker to authenticate as another user to escalate privilege, potentially even as root.
Source: https://steflan-security.com/linux-privilege-escalation-exploiting-misconfigured-ssh-keys/

4- [[Sudo Shell Escaping (Escalation)]]
Sudo is a very important command in Linux admin toolset. It allows a regular user the privilege to execute commands otherwise only super user (Super User Do) could do.
These privileges could be abuse by taking advantage on some flaws.
Check out GTFOBins - [https://gtfobins.github.io/](https://gtfobins.github.io/) for details

5- [[Escalation via LD_PRELOAD]]
On most Linux system, there is a mechanism called preloading. LD_PRELOAD is a environment variable flag set to utilize the mechanism of preloading. This could also be a security risk. LD stands for Link Dynamic. 