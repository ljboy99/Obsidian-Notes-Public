**IP Addressing on Hosts**

**Dynamic Host Configuration Protocol**
DHCP leases IP addresses to devices. This is done conveniently without making users ask for network information to do manual configurations. 
Hosts start with no IP, mask, default router or DNS server. They follow DORA to get them:
**Discover** - Client looks for server
**Offer** - Server offers IP and other information
**Request** - Client asks server to lease IP and other information 
**Acknowledgement** - Server assigns mask, router, IP and DNS.

Because it does not have an IP, the host will send packets to the DHCP server under the IP 0.0.0.0, and uses the broadcast address 255.255.255.255 as a destination.
More or less, it just screams into the void and hopes a DHCP server answers.
DHCP server will also use 255.255.255.255 because the host it's talking to still has no IP. The message will contain the hosts MAC address so there's no confusion. 

**APIPA IP Address**
If the DHCP process fails, a host will eventually assign it's own IP as a backup.
It will be within the range of 169.254.x.x and only be able to communicate within the local network. 

**Supporting DHCP for Remote Subnets with DHCP Relay**
Engineers choose between setting up DCCP's on every router or having just one central DHCP server.
Cisco recommends the latter, but you need a way to get DHCP messages from a local network to the server. 
This is done with the following command:
```
ip helper-address (server ip address)
```
This reroutes local data to the DHCP server by changing the destination IP.
Ultimately this command will change the data that from 0.0.0.0 and to 255.255.255.255 to being from the router IP to the DHCP IP.
This also works in revers, because when routers get data with destination of their IP, they realize its for a host in their connected local network, and changes the destination to the broadcast address 255.255.255.255

**Information Stored at the DHCP Server**
The DHCP server maintains a pool of information that's ready to be distributed to hosts. To do it's job, it also has to know subnet ID's, masks, reserved addresses, default router IPs and DNS IPs. This helps the server know what and what not to lease. 

DHCP has 3 allocation modes:
- Dynamic allocation
- Automatic allocation
- Static allocation

**Configuring DHCP Features on Routers and Switches**
Routers can be DHCP servers, or function as relays for a separate standalone DHCP server
Routers and Switches can both be clients of a DHCP server, getting IPs and Configs from them

**Configuring DHCP Relay**
DHCP Relays are set up when DHCP servers live outside the subnet where DHCP clients are. This is done with the following command
```
ip helper-address (server ip)
```
You can view your routing configuration file to determine if a helper address is currently set. 

**Configuring a Switch as a DHCP Client**
To configure DHCP on a switch, navigate to interface configuration mode and enter
```
ip address dhcp
```
Once assigned, you can see the IP with:
```
show interfaces vlan (number)
or
show dhcp lease
```
**Configuring a router as a DHCP Client**
(This usually only makes sense to do with routers that will be connected to the internet. )
Despite not directly using gateway IP addresses, a router can build a default route with that information. 
This essentially assigned the ISP to the be the next hop. 
A router can also share this route with other routers. 

Once you set up and interface with the command "ip address dhcp" it will automatically learn that default route.

**Identifying Host IPv4 Settings**
IPv4 hosts need: 
- DNS IP's
- Default gateway IP
- Their own IP
- Their own Mask
The devices need these in order to function on the network. 

Most OS's will have a GUI where you can view this network information. You can otherwise utilize their CLI interfaces with the appropriate commands for their OS.

For example, on windows you can view some network info with "ipconfig /all" and look at the results to look for configuration errors or DHCP failures 