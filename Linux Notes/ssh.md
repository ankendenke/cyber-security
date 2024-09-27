#SSH (secure shell) is a secure protocol used as the primary means of connecting to #Linux [[Linux]] servers remotely.  The connection is made by providing asymmetric cryptographic mechanism, using private key (use to encrypt the data), and a public key (use to decrypt the data).
The private key must stay on the client's computer and only accessible to the key owner, whereas the public key is available on the remote computer.

When you connect through SSH, you will be dropped into a shell session, which is a text-based interface where you can interact with your server. For the duration of your SSH session, any commands that you type into your local terminal are sent through an encrypted SSH tunnel and executed on your server.

##### How SSH Authenticates Users

Clients generally authenticate either using passwords (less secure and not recommended) or SSH keys, which are very secure.

Password logins are encrypted and are easy to understand for new users. However, automated bots and malicious users will often repeatedly try to authenticate to accounts that allow password-based logins, which can lead to security compromises. For this reason, we recommend always setting up SSH key-based authentication for most configurations.

To authenticate using SSH keys, a user must have an SSH key pair on their local computer. On the remote server, the public key must be copied to a file within the user's home directory at `~/.ssh/authorized_keys`

##### Generating an SSH Key Pair
The first step to use key pair method
```
ssh-keygen
```
Entering  a passphrase of an arbitrary length adds additional security to your private key. But you should remember it of you want change or alter the key.
```
ssh-keygen -p # change the passphrase added at the creation of the key
```

This procedure has generated an RSA SSH key pair, located in the `.ssh` hidden directory within your user's home directory. These files are:

- `~/.ssh/id_rsa`: The private key. DO NOT SHARE THIS FILE!
- `~/.ssh/id_rsa.pub`: The associated public key. This can be shared freely without consequence.

##### Displaying the SSH Key Fingerprint

This command allows to display the key fingerprint.
```
ssh-keygen -l 
```
##### Connecting to a Remote Server
To connect to a remote server, the user must exist. 
```
ssh remote_host 
```
```
ssh username@remote_host # if the username is different on the remote server
```
Source: https://zah.uni-heidelberg.de/it-guide/ssh-tutorial-linux

Config file for sshd
```
/etc/ssh/sshd_config
```
Allow change to port, authentication, etc
