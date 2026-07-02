## **Troubleshooting IPv4 Routing**

### Strategies and Results when Testing with ping
##### Testing Longer Routes from Near Problem Source
Sometimes in IT, you dont have direct access to a machine where a problem is occuring. You can often investigate the network by pinging  routers and ruling out routing issues. You can also issue pings from a customers router remotely. 
For example, a working ping from a router when there's issues inside the network confirms that there aren't issues affecting the network from outside the boundary. 
It can also tell us whether a single device is affected because we can ping other devices in the network. 
It can also confirm the working status of switch and router interfaces and connect filter configurations. 

##### Using Extended Ping to Test the Reverse Route
Your standard pings test for connectivity of a route going one one, and not the reverse route going back to the original device. 
A 2 way test can be done with an extended ping because youre able to add more details and configurations to your ping request, such as the source of the ping and where to ping back to.

##### Testing LAN Neighbors with Standard Ping
A working ping shows that devices can pass frames and learn MAC addresses properly, among other things. 
Ping failures can be a symptom of issues with IP addresses, masks, DHCP, trunking, LAN and more. 

##### Testing LAN Neighbors with Extended Ping
Extended pings can test default router settings. 
Standard ping tend to lean to the most efficient interface, while extended pings let users select what port to ping from.

##### Testing WAN Neighbors with Standard Ping
A successful ping between two routers with a WAN link between them tells us that the interfaces are up/up and the units are correctly configured. 

##### Ping with Names and IP Addresses
You can ping hostnames to undergo tests involving DNS such a s pinging a domain to check for DNS issues.
You can locally configure hostnames with the command
```
ip host (name) (address)
```
This will teach your router or switch to resolve that name to the specified address.
ex.
```
ip host HOSTB 172.16.2.101
```

### Traceroute
Like ping, traceroute is a tool to test connectivity and get devices to reply
Traceroute can take more time to use but can provide you with more details. 
Unlike ping, traceroute can show you how far a packet makes it through transmission before it's discarded. 
It will list each next-hop address. 

##### How Traceroute Works
Traceroute works to trigger error messages to identify routers in a transmission route
It utilizes the ICMP TTL Exceeded error to achieve this, simply by sending packets with low TTL values to trigger that error and identify router IPs based on where the error comes from.
To make sure it gets to see the entire route, traceroute will slowly increase the TTL timer to make sure it gets errors from more routers. Starting with a TTL of 1, then 2, 3, 4, so on. 

##### Standard and Extended Traceroute
Traceroute has different options and configurations. 
Standard is easier and classes things based on how packets would normally flow. 
Extended traceroutes let the user configure things like server IP, TTL, probe count, etc.
Traceroute syntax may vary based on OS.

### Telnet and SSH
You can use telnet or ssh to perform tests on the behalf of other devices by logging into them remotely. 
Login by telnet:
```
telnet ip-address
```
The CLI will then prompt you to login by username and password to the device. 
SSH:
```
ssh -l usename host-ip
```
Here, you already specified your username, and will be prompted by the CLI to enter your password to get into the device. 
The 'exit' or 'quit' command will log you out of the device when you are done with your telnet or SSH connection.



