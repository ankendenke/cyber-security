#### What's Linux
Open source Operating System (OS)

OS is responsible for resource management:
- Processor time
- Memory management
- Storage space

Linux is just a Kernel or core of the OS
- Lowest level

###### Linux Distro:
Think of ice cream flavors:
- Debian
- Ubuntu
- Fedora
- Linux Mint
- CentOS
- RedHat
- Kali
- ParrotOS
- SuSe
- Gentoo OS

#### Intro to Command Line
The Linux command line is the most interactive function of the systems. It's called the Shell, and is characterized as follow:

```
username@computername:<current directory>$
```
Ex:
```
medtraore@laptop-pc:~$
```
~ is the home directory of the user

###### Some Commands
*whoami* - returns the current username
*hostname* - returns the computer name (host)
*pwd* - returns the current working directory
*ls* - list the content of the directory
ls --ignore='File*' or ls -I 'File*' list all the file in the current directory expect 'File*', or exclude 'File*' from the list on the current directory

*cd* - change directory

## Getting Help
A manual is available on the shell
*man* - access the manpage 
*man* <command name> - access the manual of the specified command name
*info *<command name> - another way to access help on <command name>
<command name> help - another way to get help on <command name>

##### Online:
https://explainshell.com - very useful website to explain shell command in a nice way
##### Looking at text: more or less
*more* - see inside a text file. You can only move forward. Type 'q' to exist
*less* - see inside a text file. You can use down, up arrow as well as pg up/pg dwn to move.
*cat* -- concatenate. Use to print the content of one or more text file

##### Linux File System
Although each distribution can organize their file system however they like, most distro follow the Linux Filesystem Hierarchies
man hier for more information
Note that unlike Windows, their is no drive letter (C:, D:, etc) instead, / (root directory is used to organize the filesystem.



| Directory | Description                                                       |
| --------- | ----------------------------------------------------------------- |
| /         | - Root directory                                                  |
| /bin      | - Important executable programs (command like more, less, etc...) |
/ boot| - All the files needed to boot the system, such as the kernel image etc... These files are managed by the system itself, you probably don't need to manage any of them. |
|/dev | - All files in this directory representing devices connected to the system. Do not play around this directory|
|/etc  | - Contains configuration files, representing divers services and devices. It's important to be familiar to what is in there. |
|/home |- Contains personal directories of all users on the system.|
|/lib|- Contains important directories needed to run programs| 
|/media|- This the directory where usb, cd are mounted|
|/mnt|- Host temporary filesystem. It's used to be utilized for media file like CD, USB|
|/opt|- Contains software installed not by the distro package management system.|
|/proc|- Contains files for running process|
|/root|- Home directory of the root user.|
|/sbin|- Like /bin directory, but only used by the root or super user.|
|/tmp|- Contains temporary files used by the system. The contain can be deleted at any time, it's so volatile.|
|/usr|-  Contains a number of subdirectory, one the most important is /usr/bin which contains important commands like ls, also /usr/local is used to install some program for the system.|
|/var|- Contains subdirectory. /var/log is one the most important. /var/log/syslog contain system informations, can be used for troubleshooting purposes.|
 
  
##### Devices, Partitions and Mounting
As stated previously, Linux doesn't use drive letter.
**sda** - First sata drive (a)
**sdb** - Second sata drive (b)

Partitions or volume are also numbered likewise on the drive where they reside
***sda1*** - First partition on the first sata drive 
***sda2*** - Second partition on the first sata drive
#####  Useful filesystem commands
***less*** /etc/fstab
***mount***
***df -h*** - Displays the disk usage 
***du -sh*** - Displays the usage of each directory

#####  Working with Files and Directories
***touch*** -  Update the access and modification times of each FILE to the current time. If the file doesn't exist, the file is created.
***cp*** - Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.
***mv*** - move (rename) files
***rm*** - remove files or directories
***mkdir*** - make directories. Create the DIRECTORY(ies), if they do not already exist.
***rmdir*** - remove empty directories

##### Spaces in the file and directories names
The best practice is not to use spaces, but if you don't have a choice, the best alternative is to use double quote. For example ls "file with space.txt". Single quote also works, but if there is a special character in the name, the shell may interprets it differently.

##### Globbing
- [ ] TO Do some future research on the topic 

Bash manual chapter on shell expansions: https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Shell-Expansions

##### More looking at text file
***head*** - output the first part of files (5 line per default)
***tail*** - output the last part of files (5 line per default)
***diff*** - compare files line by line, Compare FILES line by line.

##### Hard and Soft Filesystem Links
ln - make links between files, In  the 1st form, create a link to TARGET with the name
       LINK_NAME.  In the 2nd form, create a link to TARGET in
       the  current directory.  In the 3rd and 4th forms, cre‐
       ate links to each TARGET  in  DIRECTORY.

#####  Compressing and Archiving Files
***zip*** - package and compress (archive) files 
***unzip***  -  list,  test and extract compressed files in a ZIP archive
***tar*** - an archiving utility Traditional usage
```
       tar {A|c|d|r|t|u|x}[GnSkUWOmpsMBiajJzZhPlRvwo] [ARG...]
```
```
example: tar cvf backup.tar file1.txt file2.txt dir? shakespeare.txt
```
Please note that tar doesn't compress, its just archive
***gzip*** - ***gzip, gunzip, zcat*** - compress or expand files
***tar*** can be used to compress archive and compress using the 'z' option. In that case you must use the .gz as extension on the file creation.

***ncdu*** - Manage disk usage and file system
##### Searching the Filesystem
***find*** - search for files in a directory hierarchy
```
example1: find . -name 'file*.txt' - in this case single quote allows the asterisks to be interpreted as a wild card. 
```
```
example2: find . iname 'file*.txt' - in this variant the 'casing' will be taken in account.
```
***locate*** - uses a database to proceed to find a file. You can search on the entire filesystem.
***which*** - locate a command which  returns  the  pathnames  of the files (or links)
       which would be executed in the current environment, had
       its  arguments  been  given  as  commands in a strictly
       POSIX-conformant shell.
***whereis*** - locate the binary, source, and manual page
       files for a command

##### Working with users and Groups

Who is logging on the system
3 interesting commands:
***users*** - print the user names of users currently logged
       in to the current host
***who*** - show who is logged on
***w*** - Show who is logged on and what they are doing.
***usermod*** - modify a user account
```
usermod -aG append (a) the user to a group (G)  
```
Associated with the username is the password and the home directory. We can see most of these in the /etc/passwd file.
Similarly the group are configured in /etc/group

##### File and Directory Permissions
Linux uses a simple permission mechanism to ensure proper access to file and directory. We can see the permissions using:
```
ls -al
drwxr-xr-x 16 medtraore medtraore  4096 Jul 17 08:03  .
drwxr-xr-x  3 root      root       4096 Nov  9  2021  ..
-rw-------  1 medtraore medtraore 14263 May 22 09:52  .bash_history
-rw-r--r--  1 medtraore medtraore   220 Nov  9  2021  .bash_logout
-rw-r--r--  1 medtraore medtraore  3860 May 20 12:53  .bashrc
drwxr-xr-x  3 medtraore medtraore  4096 May 20 12:53  .byobu
drwxr-xr-x  5 medtraore medtraore  4096 Nov 27  2021  .local
-rw-r--r--  1 medtraore medtraore     0 Jul 15 21:56  .motd_shown
-rw-r--r--  1 medtraore medtraore   807 Nov  9  2021  .profile
-rw-------  1 medtraore medtraore   631 Dec 14  2022  .python_history
-rw-r--r--  1 medtraore medtraore    66 Dec 14  2022  .selected_editor
-rw-r--r--  1 medtraore medtraore     0 Nov  9  2021  .sudo_as_admin_successful
-rw-------  1 medtraore medtraore  3658 Dec 17  2021  .viminfo
drwxr-xr-x  5 medtraore medtraore  4096 Dec 20  2021  .vscode-server
-rw-r--r--  1 medtraore medtraore   165 Dec 23  2021  .wget-hsts
-rw-r--r--  1 medtraore medtraore  1933 May 17 14:12  .wsl-config
drwxr-xr-x  5 medtraore medtraore  4096 Nov 14  2021  Junk
drwxr-xr-x 62 medtraore medtraore  4096 Nov 12  2021  Photos
drwxr-xr-x  2 medtraore medtraore  4096 Nov 14  2021  bin
drwxr-xr-x  5 medtraore medtraore  4096 Dec 15  2022  datacamp
drwxr-xr-x  3 medtraore medtraore  4096 Nov 14  2021  derekbanas
drwxr-xr-x 16 medtraore medtraore  4096 May 17 13:58  dradis-ce
-rw-r--r--  1 medtraore medtraore   339 Dec 14  2022 'function_test .sh'
medtraore@medtraore-msi:~$
```

**d - stands for directory**
**- - stands for file**
**l - stands for symbolic links**

![[Pasted image 20240730101637.png]]

Source: https://delinea.com/blog/linux-privilege-escalation (image only)

Each of the 3 blocs indicate the permission status of the file or directory.
the first bloc are the perm for the owner, the second bloc perm for the group the user belongs to and the last bloc all other users or also called the world perm.
***chmod*** - change file mode bits
```
Examples:
chmod g + w 'function_test .sh' adds the write permission for the group on the file named 'function_test .sh'
chmod u - w 'function_test .sh' removes the w permission for the user on the file named 'function_test .sh'
chmod a + w 'function_test .sh' adds the write permission for the world on the file named 'function_test .sh'
chmod a=, u=x 'function_test .sh', no perm for the world and execute perm for the user.

```
***chown*** - change file owner and group
***chgrp*** - change group ownership

##### Changing Users
Passwords are stored in the /etc/shadow
to access this file we need a root access password
```
sudo cat /etc/shadow
```
***sudo, sudoedit*** — execute a command as another user
To run a command as another user,
```
sudo -u <user> cat /home/filename
```

***su*** - run a command with substitute user and group ID
This let you act as another command for multiple commands

##### Changing Passwords
***passwd*** - change user password. A normal user
       may only change the password for their own account, while the superuser
       may change the password for any account.  passwd also changes the
       account or associated password validity period.


##### Linux Package Management
Modern day Linux systems use centralized automated system for updating, installing software. It's similar to app stores. Package managers handle libraries and dependencies, so that users do not have to worry about anything.  

there are 2 main package managers, Debian based (==.deb==) and RedHat based (==.rpm==) management systems.

###### Package Management: Debian Systems
***dpkg*** - package manager for Debian, is a medium-level tool to install, build, remove and manage Debian packages.

[[apt & apt-get]]

### Package Management: RedHat Systems
[[yum & rpm]]

###### Manually Installing Software
Download and compile the program...
```
configure
make
make install

```
##### Common Command Line Shells
- ksh
- csh
- bash
- tcsh
- zsh

##### Environment Variables
***printenv*** - print all or part of environment.  Print  the values of the specified environment VARIABLE(s).  If no VARIABLE is specified, print name and value
       pairs for them all.

##### Startup Files
***.bashrc***
Bash manual chapter on startup files: https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html

##### Redirecting Input and Output
Conceptual files that are always open:
***stdin*** - send info to program
***stdout*** - default output
***stderr*** - all errors to sent to

```
ls /temp > dir_content.txt - redirects the stdout to a file called dir_content.txt
ls /home >> dir_content.txt - append the stdout to the same dir_content.txt
```
Note: if you don't append to the file, the content will be replaced by the recent command.
```

medtraore@medtraore-msi:~$ head < /etc/passwd - here we redirect the content of a file to the head command
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
Note: Most command that accept a file argument can use stdin for redirection.

```
```
find / -name 'sample.txt' 2> errors.txt - find 'sample.txt' and redirects stderr to a file called errors.txt
```
```
find / -name 'sample.txt' 2> /dev/null - find 'sample.txt' and disregard all errors
find / -name 'sample.txt' &> all.txt - find 'sample.txt' and redirects stdout and stderr to the file named all.txt
find / -name 'sample.txt' > location.txt 2> /dev/null - send the result to location.txt and the stderr to /dev/null (disregard errors)

```
##### Pipes
Redirect the output of one command to the input of another command
```
ls - al | less - output the 'ls' command as input to the 'less' command 
ls -al /etc | head -n 20 | tail -n 2 - list the 2 lines of the first 20 lines of the /etc directories

```
#####  Command History
The bash allows to repeat commands without retaping
history - list of command previously executed on the bash shell
```
!<history #> - re-execute the command at the <history #>
!! - re-execute the last command in the history library
Up and Down Arrow - Lets you navigate through the history
```

##### Command Substitution
`<command>` - the backtick is used to the shell that the expression inside is a command, as such to execute it. This is how you do command substitution
```
Example:
ls -l `cat errors.txt` - execute the cat command then return the shell to ls -l
$(<command>) - alternatively used to command substitution
```


##### Searching and Processing Text
***grep*** - print lines that match patterns
```
Example:
grep bob wordlist.txt - search for bob in the file called wordlist.txt
grep -v e wordlist.txt -  search and return all words in the file wordlist.txt except the ones containing the letter e
grep error /var/log/*.log - search the word error in the all error logs in /var/log.

```
```
grep error -B 3 -A 2/var/log/*.log - same result as previous, but display the 3 lines before the error and 2 lines after the error.
```

***sort*** - sort lines of text files
```
Example 
sort random-wordlist.txt - sort the contain of the file named random-wordlist.txt in alphabetical order
sort -nr random-numbers.txt - sort the contain of the file named random-numbers.txt in descendant order
```

***uniq*** - report or omit repeated lines (adjacent lines)
***wc*** - print newline, word, and byte counts for each file


##### Manipulating Text

***[[sed]]*** - stream editor for filtering and transforming text, manipulate text line by line
https://www.gnu.org/software/sed/manual/sed.html

```
Example
sed 's/Suite/Ste/' sample.txt - replace (substitute, the expression Suite by Ste in the file sample.txt
Note: only the first instance is being replaced.  The 'g' option at the end on the expression replace all the instance in the lane: sed - 's/Suite/Ste/g' sample.txt 

sed '$s/Suite/Ste/' sample.txt - replace only the last occurrence on the expression (the last line in the text file)

sed '/Suite/d' sample.txt - delete the expression Suite in the sample.txt file
sed 's/$\n/g' sample.txt - insert a new line at the end of record (create a space between record)
sed 's/,\n/g' sample.txt - replace each comma by a new line
sed -e 's/$\n/g' -e 's/,\n/g' - the 2 last commands executed in a single command with the 'e' option

```
https://www.gnu.org/software/gawk/manual/gawk.html
g[[awk]] - pattern scanning and processing language 
(To be reviewed in depth, search for youtube videos and google search to learn more)
[*] https://github.com/danielmiessler/SecLists - Find a better place for this in the document

***tr*** - translate or delete characters

```
Example:
cat sample.txt | tr ',' '\t' - replace commas by a tab (\t) in the sample file
cat sample.txt | tr 'a-z' 'A-Z' - replace all lower case letters by upper case letters
cat sample.txt | tr '[:lower]' '[:upper]' - same as previous command using a specific command


```
##### Networking at the Command Line
***ping*** - send ICMP ECHO_REQUEST to network hosts
***ifconfig*** - configure a network interface
***ip*** - show / manipulate routing, network devices, interfaces and tunnels
***nslookup*** - query Internet name servers interactively
***dig*** - DNS lookup utility
***[[netstat]]***  - Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships

##### File Transfer Utilities
***scp*** — OpenSSH secure file copy
***rsync*** - a fast, versatile, remote (and local) file-copying tool


##### Converting Text Files
Line terminator conversion between OSes
***file*** — determine file type
***dos2unix*** - DOS/Mac to Unix and vice versa text file format converter.

##### Text Editors: nano
***nano*** - Nano's ANOther editor, inspired by Pico. nano  is  a  small and friendly editor.
***vim*** - Vi IMproved, a programmer's text editor

##### Process Information
***ps*** - report a snapshot of the current processes.
***pstree*** - display a tree of processes
***top*** - display Linux processes updated every 3 seconds. The  top  program  provides  a  dynamic  real-time  view  of  a running system.  It can display system summary
       information as well as a list of processes or threads currently being managed by the Linux kernel.

##### Managing Processes
***kill*** - send a signal to a process. The default signal for kill is TERM.  Use -l or -L to list available signals.  	Particularly useful signals include HUP, INT, KILL, STOP, CONT, and 0.

***pgrep, pkill, pidwait*** - look up, signal, or wait for processes based on name and other attributes. pgrep  looks  through the currently running processes and lists the process IDs which match the selection criteria to std‐
       out.  All the criteria have to match.
***sleep*** - delay for a specified amount of time.

##### Scheduling Processes with Crontab and Init.d
***cron*** - daemon to execute scheduled commands (Vixie Cron)
/etc/crontab - configure the cron daemon
***crontab -e*** - edit contab and personalize it
https://crontab.guru/
***crontab*** - maintain crontab files for individual users (Vixie Cron)

##### What is a Regular Expressions?
Pattern matching. Complex pattern matching, powerful and flexible.
Regexr web site: https://regexr.com/
Regex 101 (alternative to Regexr): https://regex101.com/

#####  Searching with Regular Expressions
Regexr web site: https://regexr.com/
Regex 101 (alternative to Regexr): https://regex101.com/


###### Replacing with Regular Expressions
This varies across implementation of the Linux system


###### Bash Scripting: Basics
[[bash]]