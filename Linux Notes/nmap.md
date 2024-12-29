[[Linux]] command to scan network and discover ports, services, etc... Network exploration tool and security / port scanner

Getting Help
```bash
nmap -V
man nmap
```

Basic scan
```bash
nmap <target IP or hostname>
nmap 10.0.2.5
nmap scanme.nmap.org
```
The six port states recognized by Nmap

***open***

An application is actively accepting TCP connections, UDP datagrams or SCTP associations on this port. Finding these is often the primary goal of port scanning. Security-minded people know that each open port is an avenue for attack. Attackers and pen-testers want to exploit the open ports, while administrators try to close or protect them with firewalls without thwarting legitimate users. Open ports are also interesting for non-security scans because they show services available for use on the network.

***closed***

A closed port is accessible (it receives and responds to Nmap probe packets), but there is no application listening on it. They can be helpful in showing that a host is up on an IP address (host discovery, or ping scanning), and as part of OS detection. Because closed ports are reachable, it may be worth scanning later in case some open up. Administrators may want to consider blocking such ports with a firewall. Then they would appear in the filtered state, discussed next.

***filtered***

Nmap cannot determine whether the port is open because packet filtering prevents its probes from reaching the port. The filtering could be from a dedicated firewall device, router rules, or host-based firewall software. These ports frustrate attackers because they provide so little information. Sometimes they respond with ICMP error messages such as type 3 code 13 (destination unreachable: communication administratively prohibited), but filters that simply drop probes without responding are far more common. This forces Nmap to retry several times just in case the probe was dropped due to network congestion rather than filtering. This slows down the scan dramatically.

***unfiltered***

The unfiltered state means that a port is accessible, but Nmap is unable to determine whether it is open or closed. Only the ACK scan, which is used to map firewall rulesets, classifies ports into this state. Scanning unfiltered ports with other scan types such as Window scan, SYN scan, or FIN scan, may help resolve whether the port is open.

***open|filtered***

Nmap places ports in this state when it is unable to determine whether a port is open or filtered. This occurs for scan types in which open ports give no response. The lack of response could also mean that a packet filter dropped the probe or any response it elicited. So Nmap does not know for sure whether the port is open or being filtered. The UDP, IP protocol, FIN, NULL, and Xmas scans classify ports this way.

***closed|filtered***

This state is used when Nmap is unable to determine whether a port is closed or filtered. It is only used for the IP ID idle scan.

---

[Prev](https://nmap.org/book/man-host-discovery.html)
Host Discovery 

You can multiple targets, CIDR, or a range of ip addresses
You can also scan a list of IP addresses from a text file: each entry of the file should separated by tab, space or newline

```bash
nmap -iL ipfile.txt
```
To exclude Host
```bash
nmap <target IP> -- exclude <target> or <ipfile.txt>
```
To use a specific network interface on your PC
```bash
nmap -e <your interface name> <target>
nmap -e lo 10.0.2.5
nmap -e eth0 10.0.2.6
```
Scan Random Target
```bash
nmap -iR <numberof random target>
nmap -iR 3
```
Shown only Open states
```bash
nmap --open <target>
nmap --open 10.0.2.6
```
Troubleshoot connectivity
```bash
nmap --packet-trace <target>
nmap --packet-trace 10.0.2.5
```
Scan fast 
```bash
nmap -F <target>
nmap -F 10.0.2.5
```
Scan specific port
```bash
nmap -p <target port> <target>
nmap -p3306 10.0.2.6

nmap -p <target port name> <target ip>
```
Scan by Protocol
U - UDP
T - TCP
```bash
nmap -sU -sT -p U:<port> T:<port> <target>
nmap -sU -sT -p U:53 T:25 10.0.2.6
```
Scan Top Ports
```bash
nmap --top-ports <number> <target>
nmap --top-ports 10 10.0.2.5
```
Perform a Sequential Scan
```bash
nmap -r <target>
nmap -r 10.0.2.5
```
Don't Ping 
```bash
nmap -PN <target> <target range or CIDR>
nmap -PN 10.0.2.6
```
Ping Only Scan
```bash
nmap -sP <target>
nmap -sP 10.0.2.5
```
Scan TCP SYN Ping
```bash
nmap -PS <target>
```
Scan ACK Ping
```bash
nmap -PA <target>
```
UDP Ping
```bash
nmap -PU <target>
```
SCTP Init Ping
```bash
nmap -PY <target>
```
ICMP Scan
```bash
nmap -PE <target>
```
ICMP Timestamp Scan
```bash
nmap -PP <target>
```
ICMP Mask Scan
```bash
nmap -PM <target>
```
IP Protocol Ping
```bash
nmap -PO protocol <target>
```
ARP Ping
```bash
nmap -PR <protocol>
```
Traceroute
```bash
nmap -traceroute <target>
```
Force Reverse DNS
```bash
nmap -R <target>
```
Disable Reverse DNS Resolution
```bash
nmap -n <target>
```
Alternative DNS lookup method
```bash
nmap --system-dns <target>
```
Manually Specifying DNS servers
```bash
nmap --dns-servers <target>
```
TCP SYN Scan Stealthy
```bash
nmap -sS <target>
```
TCP Connect Scan
```bash
nmap -sT <target>
```
UDP Scan
```bash
nmap -sU <target>
```
TCP Null Scan

```bash
nmap -sN <target>
```
TCP Fin Scan
```bash
nmap -sF <target>
```
Xmas Scan
```bash
nmap -sX <target>
```
TCP ACK Scan (to see if the system is shielded by a firewall)
```bash
nmap -sA <target>
```

TCP Customs
```bash
nmap --scanflags <target>
```
IP Scan
```bash
nmap -sO <target>
```
Ethernet Scan

```
nmap --send-eth <target>
```
Sent IP Packet
```
nmap --send-ip <target>
```
OS and Service Detection
OS Detection

```bash
nmap -O <target>
nmap -O --oscan-guess <target>
```
Service Version Detection
```bash
nmap -sV <target>
nmap -sV --version-trace <target>
```
Timing Options
Timing parameters
See https://nmap.org/book/performance-timing-templates.html

Decoy scan
```bash
nmap -D <target>
```
Idle Zombie Scan
```bash
nmap -sI <target>
```
Specific source port
```bash
nmap --source-port <target>
nmap -g <target>
```

Disable Host Enumeration
```bash
nmap -Pn <target>
```

Cool use-case with bash, select ports that are open for more investigation
```bash
ports=$(nmap -p- --min-rate=1000 -Pn -T4 <target> | grep '^[0-9]' | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
```

Then
```bash
nmap -p$ports -Pn -sC -sV <target>
```
Or
```
 nmap -sC -sV -p- -T4 --min-rate=9326 -vv [MACHINE IP]

```
Let’s break this command if it just passed up from your head 😅

- sC : run particular scripts on the target and check what all can happen there
- sV : check for the versions
- -p- : check all the ports
- -T4 : it is to speed up things(max is T5)
- --min-rate=9326 : nmap will send the packets at the rate of 9326 per second, this 9326 is just a random number that I got from my twitter friend