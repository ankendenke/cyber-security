[[Windows Privilege Escalation]] encompasses knowing which anti virus are running as well as firewall
Check if Windows defender is on (it is by default in most PC)
```
sc query windefend
```
Check all the services running on the machine
```
sc queryex
```
Check for firewall
```
netsh advfirewall firewall dump
```
or
```
netsh firewall show state
```
