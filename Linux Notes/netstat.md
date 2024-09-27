The `netstat` command lets you discover which sockets are connected and which sockets are listening. Meaning, it tells you which ports are in use and which processes are using them. It can show you routing tables and statistics about your [network interfaces](https://en.wikipedia.org/wiki/Network_interface_controller) and [multicast connections](https://en.wikipedia.org/wiki/Multicast).
```
netstat -a | less 
```

The above command displays all connections to the host
```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 10.255.255.254:domain   0.0.0.0:*               LISTEN
udp        0      0 0.0.0.0:40362           0.0.0.0:*
udp        0      0 10.255.255.254:domain   0.0.0.0:*
udp        0      0 localhost:323           0.0.0.0:*
udp6       0      0 ip6-localhost:323       [::]:*
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  2      [ ACC ]     STREAM     LISTENING     19766    /run/WSL/1_interop
unix  2      [ ACC ]     STREAM     LISTENING     17770    /run/WSL/1_interop
unix  2      [ ACC ]     STREAM     LISTENING     19771    /run/WSL/10_interop
unix  2      [ ACC ]     STREAM     LISTENING     19815    
unix  3      [ ]         STREAM     CONNECTED     17803
unix  3      [ ]         STREAM     CONNECTED     18780
unix  3      [ ]         STREAM     CONNECTED     19759
unix  3      [ ]         STREAM     CONNECTED     218      /tmp/dbus-gZjMxnEJB3
unix  3      [ ]         STREAM     CONNECTED     17829
unix  3      [ ]         STREAM     CONNECTED     17802
```
**Active Internet connections (servers and established)** :  lists the connected external connections and local sockets listening for remote connection requests. That is, it lists the network connections that are (or will be) established to external devices.

**Active UNIX domain sockets (servers and established)**: lists the connected and listening internal connections. In other words, it lists the connections that have been established within your computer between different applications, processes, and elements of the operating system.
##### Listing Sockets by Type Using the netstat Command
Only TCP type will be displayed in this command below:
```
netstat -at | less
```
Only UDP sockets type will be displayed below:
```
netstat -au | less
```
##### Listing Sockets by State
To see the sockets that are in the listening or waiting state, use the `-l` (listening) option.
```
netstat -l | less
```
This can be combined with the -t (TCP, -u (UDP) and -x (UNIX)

##### Network Statistics by Protocol
To see statistics for a protocol, use the `-s` (statistics)
```
netstat -s | less
```
This can be combined with the -t (TCP, -u (UDP) and -x (UNIX)

##### Showing Process Names and PIDs
The `-p` (program) option does just that.
```
sudo netstat -p -at
```
The above command  sees what the PIDs and process names are for the processes using a TCP socket that is in the listening state. We use `sudo` to make sure we receive all of the information that is available, including any information that would normally require root permissions.

##### Listing Numeric Addresses
We use the `-n` (numeric) option, the IPv4 addresses are shown in dotted-decimal format
```
sudo netstat -an | less
```
#####  Displaying the Routing Table
The `-r` (route) option displays the kernel routing table.
```
sudo netstat -r
```
##### Finding the Port Used by a Process
We use the `-a` (all), `-n` (numeric) and `-p` (program) options used previously, and search for "sshd."
```
sudo netstat -anp | grep "sshd"
```
Of course, we can also do this in reverse. If we search for ":22", we can find out which process is using that port, if any.

```
sudo netstat -anp | grep ":22"
```
##### List the Network Interfaces
The `-i` (interfaces) option will display a table of the network interfaces that `netstat` can discover.
```
sudo netstat -i
```
##### List Multicast Group Memberships
The `-g` (groups) option makes `netstat` list the multicast group membership of sockets on each interface.
```
sudo netstat -g
```




Source: https://www.howtogeek.com/513003/how-to-use-netstat-on-linux/
