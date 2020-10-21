> # **Practical 1**
> #####  Aim: Installation & Setup of DHCP Server
---

> ### *DHCP:* 
* The Dynamic Host Configuration Protocol (DHCP) is a network management protocol used on Internet Protocol (IP) networks, whereby a DHCP server dynamically assigns an IP address and other network configuration parameters to each device on the network, so they can communicate with other IP networks.
* A DHCP server enables computers to request IP addresses and networking parameters automatically from the Internet service provider (ISP), reducing the need for a network administrator or a user to manually assign IP addresses to all network devices.

---

> ### Steps:

> 1. Install dhcp-server:
```
sudo apt-get install -y isc-dhcp-server
```
- The server has to be configured based on the ip address. To check you ip address, the command is `ip address` or `ip a`
- You will also get info on the NIC card used. In this example we take `eth0`

> 2. Setting up the IP
```
sudo ifconfig eth0 192.168.106.128 netmask 255.255.255.0
```

> 3. Configuring /etc/dhcp/dhcpd.conf - (a)
```   
sudo nano /etc/dhcp/dhcpd.conf
```

> 4. Configuring dhcpd.conf by adding the following to the file - (b)
```
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.106.0 netmask 255.255.255.0 {
   range 192.168.106.100 192.168.106.120;
   option routers 192.168.106.255;
}
```

> 5. Next edit `/etc/default/isc-dhcp-server` 
```
sudo nano /etc/default/isc-dhcp-server
```

> 6. Edit the file according the values below:
  ```
  INTERFACESv4="eth0"
  ```
  
> 7. Enabling dhcp-server:
  ```
  sudo systemctl enable isc-dhcp-server.service
  ```

> 8. To check service status, run the command:
  ```
  sudo systemctl status isc-dhcp-server.service
  ```

> 9. To start the service, run the command:
  ```
  sudo systemctl start isc-dhcp-server.service
  ```
  
> 10. Finally, to check whether configured properly type:
```
sudo dhcpd -T eth0
```

