# Implementing Basic OSPF Features

### Implementing OSPFv2 Using Network Commands

##### OSPF Single Area Configuration 
Configuration starts with: 
```
router ospf (PROCESS-ID)
```
the PROCESS-ID should be assigned a unique value between 1 and 65,535.
Then you give network commands which tell the router to find it's peers.
If the parameters match, the router will enable OSPF on the appropriate port.

##### Wildcard Matching with the Network Command
The network command is followed by parameters for an IP, mask and area. 
The mask is a 'wildcard mask'. In this mask, the router will compare the octets that have a 0 and ignore the ones that are 255.

For example, with the command:
```
network 10.1.0.0 0.0.255.255 area (#)
```
Will compare and match up addresses that it finds starting with 10.1

##### Verifying OSPF Operation 
Useful commands include: 
```
show ip ospf neighbor
show ip ospf database
show ip route
```

"show ip ospf neighbor" will output a table of neighbor relationships to the router. 
In a single area, once neighbors are established, they should have matching databases. This can be observed with "show ip ospf database"
"show ip route" is also useful as it will tell you what routes were specifically learned by OSPF.

Some routes are established locally, some are done by OSPF. If you are unsure of whether you have the routes you need, figure out how many there should be. The amount of local routes and OSPF routes should add up to your total .

##### Verifying OSPF Configuration 
Useful commands: 
```
show running-config
show ip protocols
show ip ospf interface
show ip ospf interface brief
```
'show running-config' and 'show ip protocols' have similar info OSPF. The latter does not require privileged EXEC mode to see.

'show ip ospf interface brief' lists everything that is enabled for OSPF processing. This can help identify issues because it can let is know if some of our devices don't have OSPF enabled. 

'show ip ospf interface' will give you more detailed results than the brief version. 

##### Configuring the OSPF Router ID
```
router-id (ROUTER ID NUMBER)
```
This is the command to set a router ID number. 
If you do not set a RID, your router will choose either highest loopback address with an up status or the highest physical interface with and up/up or up/down status.

Loopbacks are virtual interfaces established through the CLI:
```
interface loopback (NUMBER)
```
It is then assigned an IP like any regular interface. Unless the shutdown command is used, a loopback interface will always have the status up/up.

Stability is important for an RID. If OSPF RID's change, it can affect neighbor relationships.

##### Implementing OSPFv2 Using Interface Subcommands
A newer command to use to enable ospf is: 
```
ip ospf
```
This essentially replaces that network command. Older interfaces may need to be converted over after their IOS is updated. 
You would start with:
```
no network (IP) (MASK) area (#)
```
and then on each interface you would use:
```
ip ospf (#) area (#)
```
This will initially break any existing neighbor relationships and then reform them as you iterate through each interface. 

##### Verifying OSPF Interface Configuration 
Interfaces configured with 'network' and 'ip ospf' show up different when you use 'show ip protocols'
the network ones will be under the label for 'routing for networks'
the ip ospf ones will be under the label for 'configured explicitly'

