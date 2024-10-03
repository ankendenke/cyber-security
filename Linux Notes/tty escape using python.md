```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

TTY Shell Stabilization Process

```bash
Victim

python -c 'import pty; pty.spawn("/bin/bash")' OR /usr/bin/script -qc /bin/bash /dev/null
Control Z

Attacker 

stty raw -echo
fg
ENTER
ENTER

Victim

export TERM=xterm
stty cols 132 rows 34
```

Source https://github.com/RoqueNight/Reverse-Shell-TTY-Cheat-Sheet

[[Linux]]
