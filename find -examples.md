`find` command, locate all the files that the user **bob** created in the past 1 minute
```
find / -user bob -type f -mtime -1 2>/dev/null
```
