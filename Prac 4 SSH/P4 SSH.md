> # **Practical 4**
> ##### Aim: SSH Server - Password Authentication. Configure SSH Server to manage a server from the remote computer, SSH Client.
---

> ## *Secure Shell (SSH)*   
*Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network.Typical applications include remote 
command-line, login, and remote command execution, but any network service can be secured with SSH.*  
`SSH client connection - Port number: 22`

> ## Steps

> 1. *Install SSH*
```
sudo apt-get install openssh-server
```

> 2. *Enable the service*
```
sudo systemctl enable ssh
```

> 3. *Start the service*
```
sudo systemctl start ssh
```

> 4. *Allow ssh by setting rules on firewall (if not installed type: `sudo apt-get install ufw`)*
```
sudo ufw allow ssh
```

> 5. *Enable the firewall*
```
sudo ufw enable
```

> 6. Check the status of the firewall, for ssh
```
sudo ufw status
```

> 7. Test the login (user, here kali)
```
ssh kali@127.0.0.1
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_or_
```
ssh kali@localhost
```

---
> To configure the ssh, the file is located at `/etc/ssh/sshd_config`. It contains options to configure the ssh. 
After configuring, restart the service, and your changes will be applied.
