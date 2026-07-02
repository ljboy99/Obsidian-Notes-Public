Broadcast frames get forwarded to all devices on a network because a switch floods it out to all ports. The span that this frame travels defines the broadcast domain.

Routers do not forward broadcast frames. Therefore, everything connected to each other before being connected to a router is considered part of a single broadcast domain.

The connection between two routers is considered it's own broadcast domain. 

To avoid too many uninvolved endpoints receiving broadcast traffic, we subnet. Splitting into separate subnets increases performance and allows for security rules between the different subnets.

Subnetted networks are still part of the same broadcast domains. They need to be separated by VLAN configured on a switch. Broadcasts in a VLAN are contained to that VLAN. 

Inter-VLAN traffic is sent through a router.

You can look at VLAN info with the following command using the 'show vlan brief' command. 

The following example will assign a range of interfaces to a VLAN:
```
interface range g1/0-3 ## this is a range of ports 0-3
switchport mode access
switchport access vlan 10
```

In terminal configuration mode, you can select a vlan to configure. 
```
vlan 10
```
This will put you in configuration mode for vlan 10.