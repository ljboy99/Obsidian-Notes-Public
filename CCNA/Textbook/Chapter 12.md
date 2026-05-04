## Classful Network Concepts

CIDR - Classless Inter Domain Routing

A CIDR block is a way of writing an IP and prefix length, separated by a slash. 

In the past, companies had 3 options to get IPs:

Public classful networks, public CIDR blocks or private classful networks. 

## IPv4 Network Classes and Related Facts

IPv4 has 5 classes. We went over A, B and C, which are unicast IPs that uniquely identify devices. 

Class D addresses are multiclass, so packets can be sent to multiple hosts. 

Class E addresses are reserved for future use.

|  Class |  First Octet | Purpose |
| --- | --- | --- |
| A  | 1-126 | Unicast (Large) |
| B | 128-191 | Unicast (Medium) |
| C | 192-223 | Unicast (Large) |
| D  | 224-239 |  Multicast |
| E  | 240-255 | Reserved |

Also, addresses beginning with 0 and 127 are reserved.

## The Number and Size of Class A, B, and C Networks

| Class | Existing Networks | Hosts per Network |
| --- | --- | --- |
| A | 126 | 16,777,214 |
| B | 16384 | 65,534 |
| C | 2097152 | 254 |

## Address Formats

Addresses in the same network match in their network part, but differ in their host parts. 

## Default Masks

These define the size of the network and host parts of unsubnetted A, B and C networks

ex. Class A IP 10.0.0.0 has a default mask of 255.0.0.0 shown in binary as

```jsx
11111111 00000000 00000000 00000000
```

## Number of Hosts Per Network

The number of host bits dictate the number of hosts by 2^H-2.

Remember that 2 addresses are reserved; One for the network ID and one for the network broadcast address. 

This is why we subtract 2 from 2 to the power of H.

## Deriving Network ID and Related Numbers

The 4 key numbers in an IP are: 

1. Network ID Number
2. First usable address
3. Last usable address
4. Network broadcast address

You can find these numbers this way:

1. Determine the IP class
2. Split the octets from network to host
3. Convert all of the host octets to 0 (This is the network ID)
4. Add 1 to the last octet (This is the first usable address)
5. Convert all host octets to 255 (This is the broadcast address)
6. Subtract 1 from the last octet (This is the last usable address)

## Unusual Network IDs and Network Broadcast Addresses

0.0.0.0 and all addresses starting with 0 are reserved addresses. 

127.0.0.1 is reserved for software testing. 

128.0.0.0 looks like a class A address but it’s actually the first class B address.