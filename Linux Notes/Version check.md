```
cat  /etc/os-release
```

```
cat /etc/issue
```

|Command|Output Example|Use Case|
|---|---|---|
|`uname -r`|`5.15.0-76-generic`|Quick kernel version check.|
|`uname -a`|Full system/kernel details|Detailed system info.|
|`cat /proc/version`|Kernel version + build details|Compiler and build time info.|
|`hostnamectl`|OS + kernel in a structured format|User-friendly overview.|