> # **Practical 7**
> ##### Aim: Install MySQL to configure database server.
---

> ### MySQL
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *It is an open-source relational database management system (RDBMS). It uses SQL (Structured Query Language) to faciliate interaction with the 
Database. In addition to relational databases and SQL, an RDBMS like MySQL works with an operating system to implement a relational database in a computer's storage system, 
manages users, allows for network access and facilitates testing database integrity and creation of backups.*

3306
Port: The TCP/IP port on which the MySQL server is listening (the default is 3306).

---

> ### Steps
---

> 1. Update apt
```
sudo apt update -y
```

> 2. Install wget
 ```
 sudo apt install -y wget
 ```
 
 > 3. Use wget to get the debian package for MySQL (since it isn't natively available on Kali Linux; the distro used here)
 ```
 sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.15-1_all.deb
 ```
 
 > 4. Install the package
 ```
 sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb
 ```
 
 > 5. Update apt again
 ```
 sudo apt update
 ```
 
 > 6. Now that we have the debian package we tell apt to manage installation of the `mysql-commmunity-server`  
 ```
 sudo apt install mysql-community-server
 ```
 
 > 7. Enable MySQL
 ```
 sudo systemctl enable --now mysql
 ```
 
 > 8. Check the status
 ```
 sudo systemctl status mysql
 ```
 
 > 9. Log in using root (?) `sudo mysql -u root -p`
 
 > 10. Start MySQL service
 ```
 sudo service mysqld start
 ```
