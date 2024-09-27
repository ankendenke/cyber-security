## **Understanding Asymmetric Encryption**
![[Pasted image 20240814114809.png]]
Source: https://vk9-sec.com/privilege-escalation-ssh-keys/

The key pair concept that #SSH and other asymmetric cryptographic protocols utilize to secure a connection is as follow:
- Private key to encrypt information: kept at the client's computer,
- Public key to decrypt information: kept on the server
When communicating to a machine via SSH, a user can authenticate if their private key is considered trustworthy by the server and added to the [authorized_keys](https://www.ssh.com/ssh/authorized_keys/) file, or if their private key corresponds to a public key stored in the server.

The default name for public keys is usually ***id_rsa.pub*** or ***id_dsa.pub*** and the default name for private keys is ***id_rsa*** or  ***id_dsa***, based on the encryption algorithm used. DSA is known to be insecure.
## **Exploiting SSH Keys**

The main two ways of exploiting SSH keys are the following:

- Accessing readable private SSH keys and using them to authenticate
- Accessing writable public SSH keys and adding your own one to them to authenticate

If readable private keys or writable public keys are present on the machine, this could allow for an attacker to #escalate #privileges to #root.

Public and private keys are generally stored in one of the following locations:

- /root/.ssh/
- /home/user_name/.ssh/ (users home directory)
- /etc/ssh/
- in the paths specified in the ssh_config or sshd_config config files

The following command can be used to identify any existing public or private keys and their permissions:
```
ls -la /home /root /etc/ssh /home/*/.ssh/; 
locate id_rsa; locate id_dsa; 
find / -name id_rsa 2> /dev/null;
find / -name id_dsa 2> /dev/null; 
find / -name authorized_keys 2> /dev/null; 
cat /home/*/.ssh/id_rsa; cat /home/*/.ssh/id_dsa
```
Private keys are used by users to authenticate via SSH. If a private key is stored in a way that makes it accessible to the current user, this means it can be used to perform an authentication as the owner of the private key.

In order for the private key to be accepted by SSH, it needs to be only readable and writable only by its owner, otherwise it will complain that the permissions applied are too open.

Using the following command to change the file permissions against the newly created SSH private key:

```
chmod 600 key_name
```

Resources:
https://vk9-sec.com/privilege-escalation-ssh-keys/
https://steflan-security.com/linux-privilege-escalation-exploiting-misconfigured-ssh-keys/