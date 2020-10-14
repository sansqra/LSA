> # **Practical 6**
> ##### Aim: Configure NTP, Install and Configure NTP Server, Configure NTP Client.
---

> ### Network Time Protocol
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *The Network Time Protocol (NTP) is a networking protocol for clock synchronization between computer systems over packet-switched, 
variable-latency data networks. NTP is intended to synchronize all participating computers to within a few milliseconds of Coordinated Universal Time (UTC). 
It uses the intersection algorithm, a modified version of Marzullo's algorithm, to select accurate time servers and is designed to mitigate the effects of 
variable network latency.*

NTP Port number - 123

A simpler version of NTP has been defined known as SNTP (Simple Network Time Protocol) as full implementation is complicated for many systems.

---

> ### Steps
---

> 1. Update apt
```
sudo apt update
```

> 2. Install ntp
```
sudo apt install ntp
```

> 3. Install sntp
```
sudo apt install sntp
```

> 4. Type the following commands consecutvely
```
sudo sntp --version
cd /etc
ls -lrth *ntp.conf*
```

> 5. Startup ntp and check its status
```
sudo systemctl start ntp

sudo systemctl status ntp
```

> 6. Configure ntp
```
sudo nano /etc/ntp.conf
```

> 7. Scroll to the following line and make the required changes, save and exit.
```
# You need to talk to an NTP server or two (or three)
server localhost
```

> 8. Check the conf file
```
cat ntp.conf
```

> 9. Restart the service
```
sudo systemctl restart ntp
```

> 10. Check status of the service
```
sudo systemctl status ntp
```

> 11. Query NTP to check connection.
```
sudo ntpq -p
```
