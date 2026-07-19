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