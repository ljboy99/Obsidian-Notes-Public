# Understanding OSPF Concepts

### Comparing Dynamic Routing Protocol Features
Definitions: 
- Routing Protocol: messages, rules, and algorithms used to learn routes
- Routed / Routable Protocol: protocol that defines what packets can be routed (ex. IPv4 or IPv6)
- Convergence: When routers see changes in topology and advertise their routing changes to each other. This is how routers learn what routes are dead. 
- Autonomous System: A network controlled by a single organization.

##### Routing Protocol Functions: 
- Learn about subnets for neighbors
- Advertise routing and subnet info to neighbors
- Pick most efficient routees
- React to changes in topology by readvertising

### Interior / Exterior Routing Protocols
Interior Gateway Protocols (IGP) are made for use within a single AS.
Exterior Gateway Protocols (EGP) are made for use between multiple different AS's
Currently there is only one EGP: Border Gateway Protocol (BGP)
AS's have number identities decided by the IANA. These are ASN's or Autonomous System Numbers.

##### IGP Routing Protocols Algorithms
The three main RPA's are:
- Distance Vector
- Advanced Distance Vector
- Link-State

The slowness of Distance Vector Protocols lead to the development of Link-State protocols which include: 
- Open Shortest Path First (OSPF)
- Intermediate System to Intermediate System (IS-IS)

Cisco also made a protocol called Enhanced Interior Gateway Routing Protocol, which functioned like Link-State, using less CPU resources. 

**Metrics**
- RIP counts hops between router and subnet
- OSPF totals bandwidth costs between points. 

### OSPF Concepts & Operation
Routers learn about networks and share the information to each other so everyone has the same info.
This information is held in data units called Link State Advertisements. 
These LSAs are held in a Link State Database by the host.
Routers will check if neighbors have the same LSA before forwarding to them. This avoids loops.

Routes aren't built just out of LSA data, but by math. Routers use Dijkstra's SPF Algorithm to build routes based off their LSDB.

Routers go through three phases in OSPF
Phase one is to become an OSPF neighbor. Routers on the same link and using OSPF can become OSPF neighbors if they have compatible parameters. Relationships with neighbors can be viewed with the following command:
```
show ip ospf neighbor
```

##### Meeting Neighbors and Learning Their Router ID.
When meeting neighbors, routers share OSPF Hello messages containing their Router ID.
Often times, an interface IP is used as the RID by default. 

##### LSDB Exchange with Neighbors
Once both routers receive an OSPF Hello, they move into a 2-way state where the Link State Database may be exchanged. 
The neighbors show each other what LSA's they have, and exchanges whatever LSA's the other doesn't already have. 
Routers will only ever request LSAs that they don't have. 
LSAs are sent through Link State Update packets (LSU packets)
Once exchange is complete, the routers will go from 2-way to a Full State.

**Maintaining Neighbors and LSDB**
The relationship is maintained with a Hello interval and a Dead interval.
Hellos are sent once every Hello interval. If a Hello is not heard by the  time the Dead interval (4x the Hello interval) is over, then it is assumed that the link has failed. 

Neighbors keep each other updated as topology and LSU's change.
They will also periodically reflood already shared LSAs every 30 minutes by default.