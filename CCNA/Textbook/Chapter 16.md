**Operating Cisco Routers**

Routers forward packets through a network. 

Installing Enterprise Routers:
Enterprises can be comprised of several locations that need their networks to work together. 
A router will usually connect the switches at each site to other routers that will relay info to their connections. 

Cisco Router Operating Systems:
Cisco routers use IOS or IOS XE

They both run a CLI end user interface. IOS XE tends to run more efficiently. 

Cisco Integrated Services Routers: 
Modern routers integrate features beyond just layer 3 routing, such as WiFi, VOIP service, LAN switching and more. 

Some routers have switching functions integrated. 

These multifunctional routers can be referred to as Integrated Services Routers or ISRs. 

Cisco Catalyst Edge Platform: 
Catalyst Edge was Cisco's next evolution of routers, successor to the ISR.
These devices, while primarily used for routing, are meant to be thought of as "more than just routers".

**Physical Installation of A Cisco Router**
1. Connect RJ-45 connectors for Ethernet LAN Interfaces
2. For Serial WAN ports, connect router (or CSU/DSU) to line from Telco
3. For Ethernet WAN:
	1. Confirm Ethernet and SFP types
	2. Install SFPs and connect Ethernet Cables
4. Connect console port to PC to configure device via the CLI
5. Connect power cable and power on the router. 

**Installing SOHO Routers**
SOHO's will more commonly be installed in homes or small offices, hence the name. 
Unlike enterprise routers, SOHO's almost always use the internet for data transfers and usually use multifunction devices that handle switching, VPNs, Wifi, etc. 

They overall simplify network equipment for small organizations that don't have heavy networking needs. 

**Accessing Router CLI**

Common Router Features
- user / privileged mode
- configuration mode
- Telnet, passwords, secrets, encryption
- hostname and description configurations
- Interface config modes.

Routers configure Telnet and SSH the same way that switches do. It's a good idea to check what is enabled by default when setting up a new device. 

**Router Interfaces**
Routers support many other interfaces aside from Ethernet. 
Some routers use serial interfaces to make serial links. 
In the CLI, you call on an interface by typing "interface", the interface type, and the port number.
Example 
```
interface gigabitethernet 0/1/0
```

You can see router interfaces with:
```
show ip interface brief
### or ###
show interfaces
```

**Interface Status Codes**
Each interface needs both of it's status codes to be "up" to work. This can also be referred to as up/up.

1. Line Status refers to physical properties like power and cabling.
2. Protocol Status refers to configurations.

These two statuses can be any combination of up or down, but, again, only function in up/up status. 

Common issues include missing or bad cables, misconfigurations, shutdown commands, etc. 

**Router Interface IP Addresses**
Sometimes, router interfaces are disabled by default (equivalent to the 'shutdown' command)
They also don't come pre-configured with IP addresses and masks. 
The "show protocols" command can help confirm the statuses of the router ports. You often want to check this on new routers, along with your IP interface brief.

**Ethernet Interface Autonegotiation**
When setting up a router, make sure your Ethernet cabling supports the distance of cable you will be using. 
To utilize different speeds you will need to either enable autonegotiation or manually set speeds. 

IOS ROUTERS:
```
configure terminal
interface g0/0
speed auto
duplex auto
```

IOS XE:
```
configure terminal
interface g0/0
netotiation auto
```

Also make sure that the connected switch or device is also set up for autonegotiation. 

**Manual Speed Configuration**
If you're using autonegotiation, make sure it's enabled on both sides of the connection.
If you're going to set speeds manually, make sure to do so on both sides of the connection. 

IOS ROUTERS: 
```
conf t 
int g0/0
speed 1000
duplex full
### REPEAT THIS PROCESS ON THE CONNECTED SWITCH INTERFACE ###
```

IOS XE:
```
conf t
int g0/0
no negotiation auto
speed 1000
duplex full
### PERFORM THE IOS PROCESS ON THE CONNECTED SWITCH INTERFACE ###
```
Notice that on IOS XE, you must manually disable autonegotiation before setting manual speeds and duplex.

**Router Auxiliary Port**
The Aux port is used to make a phone call to a router and issue commands from the CLI
It connects to a modem, which connects to a PC that is equipped with a Terminal Emulator. 
