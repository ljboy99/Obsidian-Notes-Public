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

