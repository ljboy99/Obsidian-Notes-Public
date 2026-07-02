**VLAN Routing With Router 802.1Q Trunks**

ROAS gives a router an interface to connect to each VLAN. This Can give the router a Unique IP for each ULAN. 
This is done through a single physical connection by utilizing virtual subinterfaces, each having their own IP address. 

Examples of subinterface names may be G0/0/0.10 or G0/0/0.20. Remember that these live on the same virtual interface. 

**How To Configure 802.1Q Trunking on a Router**
1. In global configuration mode:
```
interface type number.subinterface
```
2. Enter subinterface configuration mode and use
```
encapsulation dot1q vlan_id
```
3. Use
```
ip address <address> <mask>
```

**Define a Native VLAN**
a. Configure IP on interface without encapsulation command
or
b. Configure ip followed by 
```
encapsulation dot1q <vlan-id> native
```

**Verifying ROAS**
You can use either:
```
show ip route [connected]
or
show vlans
```
If interfaces are up/up, they will appear in the routing table.

This will also show sub-interfaces if their parent interface is up. 
'show vlans' command will show what interface a vlan is using to trunk. 
It will also show you the native VLAN

**Troubleshooting ROAS**
Misconfigurations on either side of the link can cause a trunking failure.
Check both sides of the link if there are issues. 
Make sure the same VLANs exist on both sides of the link. 
Make sure devices are not configured with 'shutdown' command. 

**VLAN Routing with Layer 3 Switch SVIs**
Layer 3 switches do both layer 2 switching and layer 3 routing.
This can route between VLANs unlike regular switches.

**Configuring Routing with Switch SVIs**
L3 switches will be set up with virtual interfaces to connect to each VLAN and have IP's and masks. 
These are 'switched virtual interfaces' or SVI's, and they are what move things between each VLAN. You will have one SVI per VLAN.

**Troubleshooting Routing with SVI's**
L3 switches use autostate, which looks deeply into VLAN info or 'no autostate', which does less checks. 

To be up/up in autostate:
1. VLAN is defined.
2. Switch needs one up/up interface with that VLAN.
3. VLAN is not shutdown. 
4. VLAN interface is not shutdown.

With autostate off or disabled, the switch only checks for a valid VLAN. 

**VLAN Routing with Layer 3 Switch Routed Ports**
Layer 3 switches can assume the role of a default router for endpoints. 
Instead of sending a packet out to a router, the layer 3 switch may send to it's own SVI to perform functions internally.
L3 switches can also swap functionality on a port, making one act like a router interface instead of a switch interface. 

**Implementing Routed Interfaces on a Switch**
If there's only one link to an L3 interface, a routed port can be used. 
To change a switch interface to a routed interface use: 
```
no switchport
```
Then configure IP and mask like a router port. 
This port will respond accordingly to commands like:
```
show interfaces
show ip route
```
Instead of a VLAN, this port will show as "routed" in the brief. 
Remember, routed ports are mainly good for point-to-point links. Otherwise you'll most likely want to use an SVI.

**Implementing Layer 3 EtherChannels**
Many times, engineers opt to use parallel links between some switches. 
To reduce the need to double route learning and other tasks, EtherChannel treats link pairs as single links. 

Combining routed ports and EtherChannel:
1. Configure physical interfaces
	a. make each port routed with 'no switchport'
	b. add ports to channel with 'channel-group # mode on'
	Use the same number on all interfaces of the same switch. 
2. Configure PortChannel
	a. Use 'interface port-channel #' to move into configuration mode
	b. Use 'no switchport'
	c. Configure IP w/ 'ip address *address mask*'

Remember, that IP address you configure will be applied to the port channel and not the individual interfaces. 

**Troubleshooting Layer 3 EtherChannels**
Consider: 
- Channel-group command
- Matching settings on the different interfaces
Make sure whether you enable EtherChannel statically or dynamically.
Make sure all necessary ports have 'no switchport' applied and have the same speed and duplex applied. 

**VLAN Routing on a Routers LAN Switch Ports**
Some routers have switch ports embedded into them.
These are made with things like small offices in mind. 
They are also good for budgets and require less cabling. 

**Configuring Routing for Embedded Switch Ports**
SVI interfaces are sued to combine switching and routing processes.
Configuration process:
1. Configure VLANs
	a. 'vlan #'
	b. 'switchport access vlan #'
	c. 'no shutdown'
	repeat this process for each interface.
2. Configure SVI for each VLAN used by switch ports
	a. 'interface vlan *vlan-id*'
	b. 'ip address *address mask*'
	c. 'no shutdown'
3. Configure routed interfaces with IP addresses. 
	a. use 'ip address *address mask*'
	b. configure routing protocols as needed. 

**Verifying Routing for Embedded Switch Ports**
See the following command:
```
show ip route connected
```
The output for this command will show routes with interfaces that are up/up

**Identifying Switched Ports in Routers**
Most commands to show interfaces wont make a distinction between what ports are routed or switched in a router.
The command 'show interfaces status' will show only switched ports. 
You can try to apply ip addresses, which is only accepted by routed ports. 