**Configuring IPv4 Addresses and Static Routes**

IP Routing sends IP packets from host to destination. It relies on several types of data-links.

**IPv4 Routing Process Reference**

If a destination is local, it will be sent directly to destination MAC address.
If not local, it will be sent to default gateway and forward to the MAC learned by the ARP.

Routers follow a 5 step process to routing packets:

1. If data-link frame haws no errors on FCS, it will be processed
2. Packet will be de-encapsulated
3. Router will decide a route, identify outgoing interface and the next-hop router. 
4. Packet will be re-encapsulated with new header and trailer
5. Frame will be transmitted according to the IP route.

**Example**

Host A: 172.16.1.9 /24
Host B: 172.16.2.9

Host B is outside of Host A's subnet (172.16.1.0 - 172.16.1.255), so the packet will be send to the default gateway 172.16.1.1 after being encapsulated. 

*Routing Step 1: Decide whether to process the incoming frame*
Upon receiving frames, routers will check the FCS field for errors. If there are errors, the frame will be discarded.
It also checks destination address to see if the router was meant to receive that frame; Switches sometimes flood out frames when they don't know exactly where to send to. 

*Routing Step 2: De-Encapsulation of the IP Packet*
The router will now discard the data-link header and trailer. 

*Routing Step 3: Choosing where to Forward the Packet*
The router will now consult the IP routing table looking at the facts of all available routes. 
The router will compare the destination IP with addresses defined in each subnet and match the destination to a subnet. 
This subnet will help the router know where to send the packet out to. 

*Routing Step 4: Encapsulating the Packet in a New Frame*
We now know where the packet will be going.
Now the router must re-encapsulate the frame with a new destination MAC address. 
That new MAC should either have already be learned, or will now be learned via ARP.

*Routing Step 5: Transmit the frame*
The router will now transmit the frame as soon as it can. 

**Configuring IP Addresses and Conncted Routes**
Routers need an IP address to be able to route
After being set up, routes can be learneed by:
- Connected Routes: added by IP configuration
- Static Routes: added by IP route configuration
- Routing Protocols: added dynamically by working with other routers.

**Connected Routes and the IP address command**
If an interface is in working state and has an IP, a router will add a route for it. 
This connected route is maintained as long as the connection is up/up, and discarded once the connection is shutdown.

**Common Mistakes with the ip address Subcommand**
- IP assignment may be rejected if the target is a reserved IP.
- Assigning incorrect IPs may not throw errors, but can cause communication failures with devices.
- IP assignment may be rejected if you try to connect a router interface to a subnet another interface is connceted to.

**The ARP Table on a Cisco Router**
ARP Table lists IPv4 addresses with MAC addresses of hosts in the same subnet. 
Routers refer to this table when re-encapsulating packets for new destinations. 
If not found in the table, a new ARP message will be sent to find the MAC.
Also remember that ARP table entries are removed after a certain period of time. 

**Configuring Static Routes**
Most routes are established dynamically, but sometimes, you need to set things up manually. 
You can define a static route with the "ip route" command in CLI. 
The next route you enter with this command will be added to the IP routing table. 

**Verifying Static Network Routes**
You can view static routes with the "show ip route static" command. 
This returns a table with route info like IP address, subnets, next-hops, etc. 
IOS may remove routes if it notices failures in interfaces. 

**Ethernet Outgoing Interfaces and Proxy ARP**
How Proxy ARP works: 
1. Router gets ARP request from different subnet.
2. Router has a route to forward packets to target.
3. Router can act as proxy for target host, supplying host with its MAC address.

**Static Default Routes**
When a router cant match up a packet's destination IP, it usually gets discarded. 
Default routes give instructions for cases where desitnations aren't explicitly stated. 
A static default route can be set up with the command:
```
ip route 0.0.0.0 0.0.0.0 ________
```
(The blank would be the IP of the router you are sending traffic to).
Overall, default routes are a backup so packets with incomplete destination instructions do not get discarded. 

**Static Host Routes**
Host routes are internal and point to the router that they are written on.
They have a /32 prefix
These are seldom used, but may come into play if a business needs to divert traffic or send traffic down a specific route. 
For example, you may want to route over a faster or more secure route. 

**Floating Static Routes**
Made with high administrative distance so they're only used if another route has not been successfully learned. 
They create a temporary WAN link for when a primary WAN link fails. 
An example would be using 4G/5G if a WAN link fails. 

Here's an example of setting a floating static route:
```
ip route 172.16.2.0 255.255.255.0 cell0/1/0 130
```
This would have an AD of 130, so it's ignored in preference for lower AD routes. 

**Troubleshooting Static Routes**
*Check if the routing table entry is correct*
Routers may still accept static route entries if the IP is entered incorrectly
This can result in undesirable or non-funcitonal route configurations. 
Also, if you try to set up a static route with a subnet that is already being utilized, IOS will throw an error. 

*The Static Route Does Not Appear in the IP Routing Table*
For a route to be in the table, the outgoing interface must be in an up/up state, or you need a route to the next-hop router. 
If the outgoing interface fails, the router may drop the associated route. 
You can prevend the drop by permanently adding the static route. 
```
ip route 172.16.2.0 255 255 255.0 g0/0/0 permanent
```
Keep in mind, if the interface is down, the route will fail, but will not be dropped.

**Correct Static Route Appreas but Works Poorly**
You can have a correct route, but other issues may need to be troubleshooted. 

Remember: 
- Routers tend to route toward the longest /P match
- Local routes have a 0 AD
- Host routes are /32
- Look at the ARP table with "show ip arp"
