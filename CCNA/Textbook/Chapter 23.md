# Implementing Optional OSPF Features

### OSPF Broadcast Network Type
OSPF defaults to a broadcast network type on all Ethernet interfaces. On this type, routers try to find neighbors, elect a designated router and backup designated router and also become a designated router for any subnet they're attached to with no other routers.

##### Verifying Operation with Network Type Broadcast
Note: Routers that are DROther wait to become the BDR in the event that the DR or BDR fails.

The `show ip ospf interface` command will tell you the network type, alongside the other info it presents. 

##### Using Priority and RID to Influence the DR / BDR Election
In the initial election, the highest OSPF interface priority wins. If the priorities tie, then the highest RID wins.
Once another router becomes the DR, the router that fails doesn't become DR again when it comes back online, even if it's priority is higher. 

You can set OSPF Priority (from 0 to 255) with the following command:
`ip ospf priority (NUMBER)`
If you change priority after a DR election, remember this doesn't change the DR. 

##### The OSPF Point-to-Point Network Type
Point-to-Point works well in arrangements where two routers have a single link between them. Because there are only two routers, the existence of a DR and BDR is no longer needed. Setting a network type as point-to-point let's these routers know not to participate in an election, as it would just waste time and processing power. 
A point-to-point network type can be configured with `ip ospf network point-to-point`

### Additional Optional OSPFv2 Features

##### OSPF Passive Interfaces
Normally OSPF routers continuously send Hello messages to find new neighbors. Sometimes this isn't necessary. 
A passive interface advertises is subnet, but doesn't send or receive Hello's.

You can set up a passive interface like this
```
router ospf 1
passive-interface (TYPE) (NUMBER)
```
Some routers have many interfaces, so sometimes it's better to work subtractively by making passive the default (`passive interface default`) and unassigning interfaces from being passive. Here's an example:
```
router ospf 1
passive-interface default
no passive-interface g0/0/1
no passive-interface g0/0/2
```

The latter option can be more efficient if you have several interfaces that you need to make passive.

### OSPF Default Routes
Default routes basically say "If you don't know where to send a packet, send it here".
In OSPF, the only default route usually goes to the route connected to the internet. All the other routers will learn this default. In other words, if routers don't know where a packet should go or can't match the destination to a route they know, it will send it to the router connected to the internet.

A router will need to know to advertise a default route to other OSPF routers. This is done with:
`#default-information originate`
This command will only advertise a default route if they have one in their routing table.
If you add the word `always`, the routers will still send to the edge router even if it goes down. 
`#default-intformation originate always`
This will advertise a default route to the edge router even if the edge router doesn't have it's own default route. 

Why is this important?
Because OSPF's key job is learning and sharing routes with the rest of the network, we still need to be able to do something with data that has a destination that we don't know. Once you create a route for this data, we can leverage OSPF to let the rest of the network about the default route.

Note that OSPF doesn't *create* this route, it advertises it for you. 

### OSPF Metrics (Cost)
#### Setting the cost directly
This is done with the command: 
```
ip ospf cost (#)
```

#### Setting Cost Based on Interface and Reference Bandwidth
Routers have a bandwidth setting that can be user-configured for the routers calculations, not actual transmission speed adjustments.
It is adjusted with:
```
#bandwidth (speed)
```
OSPF will use this number to calculate cost if the cost isn't explicitly configured. 

Interface bandwidth is set in kbps. It is not recommended to change your interface bandwidth number to manipulate OSPF cost. 
The issue with these calculations is that CISCO sets a default reference bandwidth of 100mpbs and rounds up any values that are less than 1, the minimum cost. 
With the formula for OSPF cost, this treats a 100 mbps and 10 gbps link as the same thing when they are truly two very different speeds. 

This is fixed by adjusting the reference:
```
#auto-cost reference-bandwidth (number)
```
The reference bandwidth is set in mbps

OSPF then calculates costs by:
`reference bandwidth / interface bandwidth`

Keep in mind, while it's useful to change the reference bandwidth it's not recommended to adjust the interface bandwidth. 

### OSPF Hello and Dead Intervals
Hello interval - interval in which Hello messages are sent to neighbors. The default is every ten seconds. 
Dead interval - Interval of how long a router should wait after not receiving a hello message to decide that a relationship has failed. This is reset every time a Hello is received. It is 4x the duration of a Hello interval, unless explicitly set otherwise.

These internals can be manually configured:
```
#ip ospf hello-interval (seconds)
#ip ospf dead-interval (seconds)
```

Remember that configuring different hello and dead intervals on two different routers can prevent them from becoming neighbors. 

IOS does not restrict or prevent you from setting a dead interval that is shorter than a hello interval. This, for obvious reasons, can be a bad idea. 

