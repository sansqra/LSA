(THIS IS A TEMPORARY FILE, UNTIL FORMATTED TO  MARKDOWN)

NIS - Directory Service Protocol

Domain name common along the entire network

MISTAKE: set domain name to kali here, instead of .com or something
-------------------------------------------------------

sudo apt-get update

sudo apt install nis (kali domain name config)


sudo nano /etc/default/nis

-------------------------------------------------------
Make server queryable. Has to be installed on both
server and client.

For demo same step twice, because can't demonstareate actual
server-client working
--------------------------------------------------------

2 types of servers : master and slave

NISSERVER=master
NISCLIENT=false

-------------------------------------------------------

will copy the /etc/default/nis file for client, only for demo
purpose, since no 2 machines

---------------------------------------------------------

sudo cp /etc/default/nis /etc/default/nis_client


-----------------------------------------------------------
Share anything that has columns
NIS has components, we will know 3.
> ypserv : yellow pages (directory). it's a server where a client
	can query to see what service is there.
> ypbind : Client binds tools
> ypxfrd : nis database is with master, this command sends the db
	to the slave (secondary server) - load balancing


----------------------------------------------------
(auth the user - settings, from IP : server side)

sudo nano /etc/ypserv.securenets

(edit accordingly)

-----------------------------------------
ip a - if you wanna put this ip in - eth0
-------------------------------------------

add this to the end (even though ip is 10.0.2.15/24)
255.255.255.0	10.0.2.0

----------------------------------------------
Initializaing yellow pages (building database)

sudo /usr/lib/yp/ypinit -m

(usually better to hamve a host name as kali.com or something
but you messed up sooo)

Ctrl + D
>>>> Error running Makefile. Please try it by hand 

which gmake
- nothing showed up

will have to set path for gmake/install it
(from gnu this gmake is - gmake only in Ubuntu)
sudo apt-get install make

dpkg -S `which gmake`
make: /usr/bin/gmake

------------------------------
> sudo /usr/lib/yp/ypinit -m

"failed to send clear" - but set up successfully on NIS

Now to check if the server is up
> sudo systemctl status ypserve
> sudo systemctl start ypserve

-------------------------------------
Still doesn't work, continue to get - "Failed to send 'clear' ..."

sudo nano /run/systemd/generator.late/nis.service
 [Install]
WantedBy=multi-user.target

> sudo systemctl daemon-reload


(error yet to be solved, steps the in this block above dont do anything)
----------------------------------------

sudo systemctl restart rpcbind nis
sudo systemctl status rpcbind

if active, then good to go.
> sudo /usr/lib/yp/ypinit -m

this should show "Updating" now, that means it works.


---------------------------------------------

Now we add user

sudo adduser n_san
psswd: nas

-------------------------------------------------
cd /var/yp
sudo make

Now this adds user to NIS. This is the server-side config

----------------------------------------------------

Now we're gonna do client config.

Client will try to resolve ther server. 
*Needs to be done on client only. But we dont have*

> sudo nano /etc/hosts

Need to add ip of client and server. (client is usually there)

We're gonna ideally put that 10.0.2.15......... but we won't, because it's
not a fully qualified domain.

If you see kali is already registered in the /etc/hosts/

Either way, gonna contradict myself, and put that ip, to see what happens

-----------------------------------------------------------
Update our client and install, nis on client. But here it's just on one
machine.
Domain name on client has to be same as server one. (Pink box or something)

> sudo nano /etc/yp.conf

ypbind thingy for client.

-----------------------
domainname -> returns domain name
----------------

gotta change server entry now, because of the stupid domain name

sudo /usr/lib/yp/ypinit -m

kali.san
ctrl+d
y

Now we have a proper domain name
-------------------------------------------
Now in client we gotta do some client stuff

sudo nano /etc/hosts

added the last entry/modified
10.0.2.15 kali.san
------------------------------------------
Now gonna edit the client conf entry

We at client machine (assume), gotta add domain and 

sudo nano /etc/yp.conf
domain san server kali.san (san / the new user n_san idk, but set to san)

how to get to kali.san, from hosts, and then resolution from yp.conf file
-----------------------------------------------

sudo nano /etc/nsswitch.conf

passwd:         files systemd nis
group:          files systemd nis
shadow:         files nis
gshadow:        files

> add nis

------------------------------------------------------
How to test whether client and server is working.

If nis service is properly up then some command on 2 terminals.

Gotta reboot, then log in, and connect

But since stuff is properly configured so far.

ping kali.san to check

--------------------
sudo reboot now

Asks user name and password

Just add the user name and password that you made.

Ideal output, since you've logged in with that add user or something

