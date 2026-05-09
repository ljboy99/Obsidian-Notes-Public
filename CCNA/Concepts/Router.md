A router is a networking device which directs packets to the optimal paths for their destinations in the [[network]]. This action, is the process of routing. 

## How Routers Route IP Packets Using Ethernet WAN Links

WANs let routers forward IP packers from one LAN, over the WAN, to another sites LAN.

When a router receives an Ethernet frame, it will remove that frames header and footer and add it’s own before further transferring the data.

This is because each encapsulation will include instructions for the next destination.

IP Routing

Network functions in TCP/IP revolve around either IPv4 or IPv6.

IP routes data in the form of IP packets. It handles the logistics of data transfer, but not the physical aspects.

## Network Layer Routing (Forwarding) Logic

Hosts use software to send IP packets to routers, which decide where the packets are going to go next.

## Host Forwarding Logic: Send Packet to Default Router.

Once a host pc looks at a packet’s desitnation and realizes it is not on the same LAN, it will then send it to a router who’s job it is to decide how to get it there.

## R1 & R2’s Logic - Routing Data Across The Network

Routers have an “IP Routing Table”. This is like a reference list of networks that it matches incoming data with to determine it's destination.

Once the router finds a match, it knows where to route data.

## Delivering Data To End Destination

Once the network layers work is done, the data is handed off to the Data-Link layer, with will create a frame for it to be sent over the physical network.

## Forwarding Logic At Each Router

1. PC1 sends packet to it's default router.
2. R1 processes frame and forwards the packet to R2
    1. Remember, R1 will remove PC1s frame and replace it with is own frame before the data is forwarded.
    2. It also uses FCS to compare the received data with what it expected to check for errors.
3. R2 processes the frame and forwards to R3
    1. Also performing reencapsulation and FCS
4. R3 processes frame, forwards to PC2
    1. Performs FCS and understands that there is no router to forward the data to the destination subnet matches it's own subnet, so it reencapsulates the data to send to PC2
    2. At this stage, R3 will also use Address Resolution Protocol (ARP) to learn PC2s MAC address so it knows where to send the data.

## How Routing Protocols Learn Routes

1. Each router adds routes for the subnets connected to it.
2. Each router tells its neighboring routers about its routing table
    1. This includes routes learned from routers it already talked to
3. Router listens to neighboring routers to learn more routes and add to it's table

Basically, a router will add it's own info to the table, tell it's neighboring routing protocol about it, and that protocol will pass it around to others until everyone is up to date.

syslog can be enabled with 
```
logging on
```
