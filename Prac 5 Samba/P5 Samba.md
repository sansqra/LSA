> # **Practical 5**
> ##### Aim: Install Samba to share folders or files between Windows and Linux.
---

> ### Samba
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *It is a free software re-implementation of the SMB (Server Message Block) networking protocol, and was originally developed by Andrew Tridgell. 
Samba provides file and print services*

---

> ### Steps
---
> ### *For Samba Server*

> 1. Install Samba server
```
sudo apt-get -y install samba
```

> 2. Start smbd, nmbd and check their status:
```
sudo systemctl start smbd
sudo systemctl status smbd

sudo systemctl start nmbd
sudo systemctl status nmbd
```

> 3. Make a directory to be shared
```
mkdir /home/kali/sambashare/
```

> 4. Creating some test files in `/home/kali/sambashare`
```
touch a.txt b.txt
```

> 5. Change direcory by typing `cd /etc/samba` and take backup of the conf file: 
```
cp smb.conf smb.conf_bkp
```

> 6. Now we conifgure the /etc/samba/smb.conf file
```
sudo nano /etc/samba/smb.conf
```

> 7. Deleting all the contents of smb.conf, add the following. (Maintain the same amount of spaces and indents)
```
[sambashare]
    comment = Welcome to Samba
    path = /home/kali/sambashare
    read only = yes
    browsable = yes
    guest ok = yes
```
* Then type `Cntrl + X`, `y`, and then `Enter`

---
> ### *For Samba Client*

> 1. Download smbclient
```
sudo apt-get -y install smbclient
```

> 2. Stop Services of smb and nmbd
```
sudo systemctl stop smbd
sudo systemctl stop nmbd
```

> 3. Check what user you are currently: `whoami`

> 4. Next `sudo pdbedit -a -u $(whoami)`

> 5. Type and retype password
```
#Checks all users

sudo pdbedit -L
```

> 6. To check your IP
```
ip a 		

(OR) 

ip addr
```

> 7. Enable ufw for Samba
```
sudo ufw allow from <ip addr> any app Samba

#here,

sudo ufw allow from 192.168.56.0/24 to any app Samba 
(or)
sudo ufw allow from 10.0.2.15/24 to any app Samba
```

> 8. Reload the firewall after adding the rules
```
sudo ufw reload
```

> 9. Restart smbd and nmbd, and check status
```
sudo systemctl restart smbd
sudo systemctl restart nmbd

sudo systemctl status smbd
sudo systemctl status nmbd
```

> 10. You can use smbclient to test samba share
```
sudo smbclient -U <username> -L  //your ip

#here

sudo smbcllient -U san -L  //192.168.56.101
sudo smbcllient -U san -L  //10.0.2.15
```

---  
> ### *Accessing Samba shared files through Windows Host OS via VM*

> 1. On the Windows Host OS, hit `Win + R` and type the smbclient ip address.
```
#here

//192.168.56.101 

(or)

//10.0.2.15
```

> 2. Now on the pop up window type your smbclient credentials.

> 3. On your File Explorer Window, you'll see `Network > <your ip_address>`

> 4. Click on the appropriate folder, here sambashare, and browse.

