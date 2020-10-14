> # **Practical 2**
> #####  Aim: Initial settings - Adding users, Network settings, Configure services and Listing services.
---

> ### Steps:

> 1. **Adding a user:**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *Most modern Operating Systems support mutli-users. And hence, using the steps below, we will demonstrate how users are added, 
on a Linux based OS.*
```
sudo adduser <username>
```

> 2. **Listing Network Interfaces:**  
* `ifconfig -a`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **or**
* `ip addr`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **or**
* `ip a`

> 3. **To enable, see status, start, restart, stop services:**
* `sudo systemctl enable <service_name>`
* `sudo systemctl status <service_name>`
* `sudo systemctl start <service_name>`
* `sudo systemctl restart <service_name>`
* `sudo systemctl stop <service_name>` 

> 4. **List running services**  
```
sudo systemctl -t=service --state=running
```

> 5. **Installing packages**  
```
sudo apt-get install <package-name>
```
