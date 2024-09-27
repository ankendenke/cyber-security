Important [[Linux]] command to monitor processes running on the local system.
**`ps aux`**: This command displays all processes for all users in a detailed format. The flags are explained below:  

- `a`: Shows processes for all users.
- `u`: Displays user-oriented format (includes user and start time).
- `x`: Includes processes not attached to a terminal (useful for finding background processes).

Let's filter out the output to show details about our `simple` process, as shown below:

**Command:** `ps aux | grep simple`  

![Shows ps aux output](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/5e8dd9a4a45e18443162feab-1726084760603.png)  

The output provides the following information:

- **USER**: The user who owns the process.
- **PID**: Process ID.
- **%CPU**: CPU usage percentage.
- **%MEM**: Memory usage percentage.
- **VSZ**: Virtual memory size.
- **RSS**: Resident Set Size (memory currently used).
- **TTY**: Terminal associated with the process.
- **STAT**: Process state (e.g., R for running, S for sleeping, Z for zombie).
- **START**: Start time of the process.
- **COMMAND**: Command that started the process.

`ps aux` can be used to get information about the running process.

Processes can be exploited, manipulated, or used by attackers to execute malicious activities. It is important to investigate the processes running on the system from various angles. The following points are a few use cases of the incidents related to processes:

- A process running from a tmp directory (context matters).
- A suspicious child-parent process.
- Process with a suspicious network connection.
- Orphan process. Not all orphan processes are suspicious, but those with no parent process associated after execution are worth investigating.
- Suspicious processes that are running through a cronjob.
- System-related processes or binaries running from the tmp directory or user directories.  
    

Investigating processes and finding a suspicious process that could indicate a potential incident is covered in detail in the Linux process Investigation room.