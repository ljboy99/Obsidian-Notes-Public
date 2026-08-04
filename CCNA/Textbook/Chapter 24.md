# OSPF Neighbors and Route Selection

## OSPF Neighbor Relationships

### OSPF Neighbor Requirements
Routers have a set of requirements to establish a neighbor connection.
This includes things like matching subnets, hello/dead timers, up/up state, etc.

### Issues That Prevent Neighbor Adjacencies
#### Area Mismatches
If routers are placed in two different areas via the CLI, they cannot be neighbors.
You can try to find the misconfigurations via `show running-config`

#### Duplicate OSPF Router IDs 
If 2 RIP's match, it will generate a duplicate OSPF RID log message. 
This can be fixed by changing one of the RID values with `router-id #.#.#.#` and then `clear ip ospf process`
So long as the RID's don't match anymore, the routers will become neighbors. 

#### Hello and Dead Timer Mismatches
If one devices hello and dead timers differ from another devices, they can't be neighbors.

#### Shutting Down the OSPF Process
The OSPF function can be turned off with the shutdown command. This kills OSPF relationships, clears the LSDB and removes OSPF routes. 

General OSPF configurations are retained even when the function is shutdown. 

#### Shutting Down OSPF on an Interface.
Rather than on an entire router, OSPF can be shut down on just a single interface. 
The OSPF configs still remain intact while shutdown. 
To do this you use the command: `#ip ospf shutdown`
This port will now stop sending Hellos and it's neighbor relationships will dissolve. 

### Issues that Allow Neighbors but Prevent IP Routes

#### Mismatched MTU
Maximum Transmission Unit defines largest packet forwarded out to the network layer
Default size: 1500
This can be changed:
	`# ip mtu (SIZE)`
	`# ipv6 mtu (SIZE)`

`# mtu (size)` can also be used to change the size for one, the other or both protocols if the previous commands don't currently exist. 
Devices with different MTU can be neighbors but this relationship will fail. 

#### Mismatched OSPF Network Type
Example: One router is point-to-point, the other is broadcast. The LSDBs will still be exchanged but the LSA's exchanged will not be able to be used by the other router. This is because they are expecting different details based on the network type that they are using. 

#### Both Neighbors use OSPF Priority 0
Priority 0 is for routers which shouldn't be DR or BDR.
The subnet always needs a designated router, but if all routers have a priority of 0, none will be elected as a DR or BDR as the role will be refused. 
Because there is no DR, the database / LSDB exchange will be halted. 

### Route Selection
#### Equal-Cost Multipath OSPF Routes
OSPF usually favors the lowest cost routes.
If multiple routes tie for the lowest cost, multiple equal-cost routes get put in the routing table. 
These multiple routes can be used for load balance.
By default, one route will be used to send to one address, and another route for a different address, splitting the routes up by destination. 

#### Multiple Routes Learned from Competing Sources
Routes are first learned as connected routes. These are commonly most efficient. 
Routes learned by other protocols will be added after. Such as OSPF or static entry.
IOS commonly uses AD or Administrative Distance as a metric to decide which routes to use. A lower AD is more efficient. By default, connected routes have an AD of 0. 
So when presented with multiple routes, IOS will look at the costs and select the most efficient ones. 

#### IP Forwarding with Longest Prefix Match
Routers compare destination IPs with the contents of their routing tables to make forwarding decisions
When only one route exists, it will be used to forward packets.
When multiple routes exists, OSPF adds them to the table and uses them for load distribution. 

##### Using Subnetting Math to Predict Choice of Best Route
With subnetting math, you can list all the possible subnets and ranges that would contain your destination address.
You can then use this list to identify the longest prefix, which is what will be preferred by the router .

#### Using `show ip route address` to Find The Best Route
This command will output what route / subnet it uses to forward to the specified address, as well as the next hop address. 


