> # **Practical 3**
> ##### Aim: Configure NFS server to share directories or files on your network.
---

> ## *Network File System (NFS)*  
&nbsp;&nbsp;&nbsp;&nbsp; *It is a distributed file system protocol allowing a user on a client computer to access files over a computer network much like local storage is accessed.*

---
> ## Steps
---
> ### For NFS Server

> 1. Install NFS server:
```
sudo apt-get -y install nfs-kernel-server
```

> 2. Making and setting permissions to the export directory
```
sudo mkdir -p /mnt/sharedfolder

sudo chown nobody:nogroup /mnt/sharedfolder

sudo chmod 777 /mnt/sharedfolder
```


> 3. Making a test file in the directory for future client side testing
```
cd /mnt/shared_folder

echo "hello world" > test.txt
```

> 4. We need to tell the NFS server that this folder exists, and give it appropriate permissions by going to `/etc/exports`
```
sudo nano /etc/exports
```
* &nbsp;&nbsp;&nbsp;&nbsp; Add the following line with the client IP (here 127.0.0.1, i.e localhost)
```
/mnt/sharedfolder <client_ip>(rw,sync,no_subtree_check)
```

> 5. Export the shared folder
```
sudo exportfs -ra
```

> 6. Restart the nfs service
```
sudo systemctl restart nfs-kernel-server
```

> 7. Allowing client IP (here localhost) to make requests to NFS, by configured traffic on the firewall
```
sudo ufw allow from <client_ip> to any port nfs
```

> 8. Check ufw status
 ```
 sudo ufw status
 ```
 
 ---
 > ### For NFS Client
 
 > 1. Install nfs-common  
 ```
 sudo apt-get install nfs-common
 ```
 
 > 2. Create a mount point for the host shared folder, to become accessible
 ```
 sudo mkdir -p /mnt/sharedfolder_client
 ```
 
 > 3. Mount the shared folder to the client side (server IP here 127.0.0.1, i.e. localhost)
 `sudo mount <server_ip>:<export_folder_server> </mnt/mountfolder_client>`
 ```
 sudo mount 127.0.0.1:/mnt/sharedfolder /mnt/sharedfolder_client
 ```

> 4. Check the client side folder, to see `test.txt` now available  
```
cd /mnt/sharedfolder_client
```
