A series of simple shell commands in a text file.
#/bin/bash - Indicates which shell to use
2 ways to run a script:
bash <script name>
or make the file executable by chmod + x <script name> and ./<script name>

```
##### Bash Scripting: Control Structures
if [condition]; then
fi

if [condition]; then

else

fi

if [condition]; then

elif [condition]; then

fi

```
##### Numeric comparison
lt - less than
gt - greater than
eq - equal to

##### String comparison
== - equal
< - less than
> - greater than

case statement
case <statement> in

esac


##### Bash Scripting: Loops
Write code once and execute repeatedly
for <statement>; do

done

##### Remote Administration
A computer can be used remotely. 
[[ssh]] -  ssh (SSH client) is a program for logging into a remote machine and for executing com‐
     mands on a remote machine.
ssh -X - GUI X with ssh 
[[remmina]] - Remmina is a remote desktop client written in GTK+, aiming to be useful for system administrators and travellers, who need to work with lots of remote computers in front of either large monitors or tiny netbooks.

