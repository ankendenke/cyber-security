A lower level priv [[Linux Privilege Escalation]] user can get out and get access to root.
https://gtfobins.github.io/gtfobins/docker/#shell
The method is simple.
The docker has be running on the system and the user has to be member of the docker group.
```
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```
