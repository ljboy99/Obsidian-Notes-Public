## Fundamentals of WANs and IP Routing

**Wide-Area Networks**

Most common WAN today in companies is Ethernet WAN. Leased-line WAN is seldom used today.

Leased Line WANs connect multple LAN routers with a WAN link. It delivers bits in both directions with Full-duplex logic. They utilize two wire pairs, one for each direction of sending data.

Leased-line WANs came about when telcos would put their equipment in a central office in a busy area, and wire it out underground to surrounding areas, hoping that they would eventually lease access to these wires as people began to do business in that area. Hence “leased” lines.

Leased-lines may also be referred to as: leased circuits, serial link, serial line, point to point link, TI, WAN-Link, Private line

[[Data Link Layer|Data-Link]] of Leased Lines

Routers on a leased line use 2 data-link protocols.

1 - High-Level Data-Link (HDLC)

2 - Point-to-Point Protocol (PPP)

These control the delivery of data over a physical link.

HDLC is only capable of sending data to the device on the other end of it’s link.

## How Routers Use a WAN Data-Link

The TCP/IP layer forwards IP packets from sender to destination in the following process:

1 - Network layer logic tells PC to send a packet to it’s router. 2 - Router’s network logic forwards that packet through a leased line to the next router. 3 - Router #2 forwards the packet to the destination PC.

Leased-lines create a WAN link between two routers so that packets can be forwarded between them.

PPP/HDLC protocols encapsulate packets to properly corss the link between two routers.

## [[Ethernet]] as a WAN Techonology

Early Ethernet was only good for about one kilometer of LAN service.

Improvements to Ethernet standards created by the IRRR increased that supported length to upwards of 70km, making is suitable for concepts like WAN.

Ethernet WAN behaves as a physical link between rotuers, creating a point-to-point connection.

## How Routers Route IP Packets Using Ethernet WAN Links

WANs let routers forward IP packers from one LAN, over the WAN, to another sites LAN.

When a router receives an Ethernet frame, it will remove that frames header and footer and add it’s own before further transferring the data.

This is because each encapsulation will include instructions for the next destination.

## IP Routing

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

## Forwarding Logic At Each [[Router]]

1. PC1 sends packet to it's default router.
2. R1 processes frame and forwards the packet to R2
    1. Remember, R1 will remove PC1s frame and replace it with is own frame before the data is forwarded.
    2. It also uses FCS to compare the received data with what it expected to check for errors.
3. R2 processes the frame and forwards to R3
    1. Also performing reencapsulation and FCS
4. R3 processes frame, forwards to PC2
    1. Performs FCS and understands that there is no router to forward the data to the destination subnet matches it's own subnet, so it reencapsulates the data to send to PC2
    2. At this stage, R3 will also use Address Resolution Protocol (ARP) to learn PC2s MAC address so it knows where to send the data.

## How IP Addresssing Helps IP Routing

### Rules for groups of IP addresses (Networks and Subnets)

Groups of IPs on the same physical Network are an IP Network/IP Subnet

These IPs will share the same numbers in the first part of their IPs

ex. 150.150.1, 150.150.2, 150.150.3

IPs in same routers must be in the same group.

IPs in different routers must be of different groups.

## The IP Header

Routing process uses IPv4 header, which carries source and destination addresses in 32-bit

Remember that this is different than Data-Link headers that are removed and replaced throughout the network routing process.

## How IP Routing Protocols Help IP Routing

Routers need to know how to route data to all reachable IP Networks.

This is possible when routers are configured with the same IP routing protocols and the same settings.

## How Routing Protocols Learn Routes

1. Each router adds routes for the subnets connected to it.
2. Each router tells its neighboring routers about its routing table
    1. This includes routes learned from routers it already talked to
3. Router listens to neighboring routers to learn more routes and add to it's table

Basically, a router will add it's own info to the table, tell it's neighboring routing protocol about it, and that protocol will pass it around to others until everyone is up to date.

## Names / Domain Name System

Sites are reachable by their IP but it's not practical to have users navigate that way.

Because of this, we use hostnames like “[www.google.com](http://www.google.com)”

A DNS would resolve a hostname request to point someone who asks for “[google.com](http://google.com)” to the IP address which hosts Googles site.

The process is as follows:

1. User asks for “[www.google.com](http://www.google.com)”.
2. DNS server responds with the IP address where Googles site info is stored.
3. Users PC sends IP packets to the provided IP address.

DNS messages are treated and transferred in the same manner as IP packets.

## Address Resolution Protocol

Ethernet LANs kinda only know what they're connected to when data is sent out. The destination MAC address is not yet known by the host or router.

LANs can learn MAC destinations by ARP

ARP request - a message asking “if this is your IP, reply with your MAC address”

ARP Reply - a response with the original (matching) IP and corresponding MAC address.

ARP replies can often be kept in an ARP cache or ARP table, which is checked before an ARP request needs to be sent.

## ICMP Echo, ping command

To test network connectivity, you may sometimes use ping.

Ping used the Internet Control Message Protocol.

It sends “ICMP echo request” to an IP

if connected, that IP will say “ICMP echo reply”

This will let you know that packets can currently be sent back and forth with that IP.