> # **Practical 5**
> ##### Aim: Install Samba to share folders or files between Windows and Linux.
---

> ### Samba
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *It is a free software re-implementation of the SMB (Server Message Block) networking protocol, and was originally developed by Andrew Tridgell. 
Samba provides file and print services*

---

> ### Steps

> 1. Install Samba server
```
sudo apt-get -y install samba
```

> 2. Make a directory to be shared
```
mkdir /home/kali/sambashare/
```

> 3. Creating some test files
```
touch a.txt b.txt
```

> 4. Change direcory by typing `cd /etc/samba` and take backup of the conf file: `cp smb.conf smb.conf_bkp`

> 5. Now we conifgure the /etc/samba/smb.conf file
```
sudo nano /etc/samba/smb.conf
```

> 5. Deleting all the contents of smb.conf, add the following. (Maintain the same amount of spaces and indents)
```
[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes
```
