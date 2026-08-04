# Introduction to IPv6
IPv6 is the successor to IPv4. It accommodates for several more address possibilities. 

#### Historical Reasons for IPv6
The internet grew very much very fast. 
So fast that we started running out of IP addresses. 
By 2010, all of the public addresses at the time were already assigned.
Eventually, no IPv4 addresses will be able to be reused, leaving only the option to use IPv6, a more permanent solution than things like NAT or CIDR.

#### IPv6 Protocols
IPv6 shares the same purpose as IPv4
Some differenced in their protocols include:
- The upgrade to OSPF version 3
- The upgrade to ICMP version 6
- ARP is replaced by Neighbor Discovery Protocol

IPv6, at most is written in 32 hex digits. Each of 4 digits are separated by a colon. 
Example: 
`2345:1111:2222:3333:4444:5555:6666:AAAA`

#### IPv6 Routing
IPv6 routing processes share similarities to IPv4.
They utilize things like encapsulation and default gateways
They packet type (ipv4/ipv6) is determined during de-encapsulation
Routers may carry a separate routing table for IPv6 addresses vs IPv4
Many enterprise networks will use both IPv4 and IPv6 as it is a slow migration. 

#### IPv6 Routing Protocols
IPv4 protocols had to be updated to support IPv6.
These now include: 
- RIP Next Generation
- OSPF Version 3
- EIGRPv6
- MP BGP-4

### IPv6 Addressing Formats and Conventions

#### Representing Full Unabbreviated IPv6 Addresses
IPv6 addresses are 32 characters with colons between every 4.

#### Abbreviating and Expanding IPv6 Addresses.
1. You may remove up to 3 leading 0's on left of a quartet
2. Replace the longest set of 2+ 0000 quartets with double colons (::)
```
EXAMPLE
2100:0000:0000:0001:0000:0000:0000:0056
2100:0:0:1:0:0:0:56
2100:0:0:1::56
```

#### Expanding Abbreviated IPv6 Addresses
1. In each quartet, add leading 0's until the quartet had 4 digits.
2. Replace (::) with additional 0000 quartets until there are 8 total quartets.

