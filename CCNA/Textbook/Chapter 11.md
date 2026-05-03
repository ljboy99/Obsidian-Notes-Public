Intro To Subnetting

Subnetting chops up a larger network into smaller parts that separate teams can use. 

There are class A, B and C IP Addresses.

Subnets divide networks. For example, a subnet of the Class B IP 172.16.0.0 could be all IPs starting with 172.16.1.0

Subnets can be assigned to LANs or WANs in the network. Subnet diagrams will notates the subnet labels and IPs.

### Operational View vs Design View

Most IT jobs will be done through an operational view because the network is designed already. 

Despite this, operators need to know how networks are designed to fulfill their duties efficiently. They need to know:

- What hosts to subnet
- How many subnets are needed
- How many IPs per subnet
- What size the subnet should be.

A rule about subnets: Any device which moves packets needs an IP address. 

Subnets are separated by routers. 

Subnets help sort messages much like how zip codes do. 

Routers are commonly configured with multiple IP address. One for each interface connection. Each IP is contained in a different subnet. 

### Determining The Number of Subnets

It’s common to have one subnet per VLAN, point-to-point serial link, and Ethernet WAN

### Determining The Number of Hosts per Subnet

Remember every device on a subnet needs an IP. 

You will want to have an idea of how many devices will be involved in the overall network when deciding on how to structure your subnets. 

### Size

Subnet size can vary, some organizations will choose to have uniform sizes for their subnets. 

Each subnet has a subnet mask which sets host bits to number host IP addresses. 

The size of the subnet may be defined by: 2^H-2, where H is the number of host bits.

The -2 in 2^H-2 represents reserved IP addresses. 

### Single-Size Subnets:

Single-Size subnets use the same mask for all subnets. 

Say your site needs 200 host addresses, the lowest viable size will be 2^8-2 (= 256) because 2^7-2 (= 128) would be less than 200

### Multiple Subnet Sizes

You can waste less IPs by having appropriately sized subnets. Some WAN links may be as small as 2^2-2.

Sizes are restricted to powers of 2 minus 2, so it’s difficult to set your size for exactly what you need.

### One Mask For All Subnets or More Than One

Some network designs use more than one subnet mask. This is a variable length subnet mask, or VLSM

### Making Design Choices

Designing a subnet is about choosing the network, choosing a mask, and then listing all of subnets in it.

First, you choose an IP network. We used to be restricted to Public IP Networks, until we introduced NAT and Private IPs so that we don’t run out of IP Addresses. This is because duplicate IP addresses can cause routing conflicts. 

The introduction of Network Address Translation allowed companies to use the same IP addresses as others in a private context, and therefore preserved many IPs. 

### Choosing an IP Network in the Design Phase

Most organizations use Private IPs and NAT. 

You just need to make sure you allot enough IP addresses for your purposes. 

Different classes of IP divide host octets and network octets differently. 

Class A has 8 network bits and 24 host bits. It’s size is 2^24-2 = 16,777,214 bits

Class B has 16 network bits and 16 host bits. It’s size is 2^16-2 = 65,534 bits

Class C has 24 network bits and 8 host bits. It’s size is 2^8-2 = 254 bits.

### Borrowing Host Bits to Create Subnet Bits

When creating a subnet, you cant change the network part or overall size of the address. You must borrow from the host end. 

For example I can subnet a class a and have an IP with 8 network bits, 12 subnet bits and 12 host bits. 

The total bits must always be 32 and you can never pull bits from the network. 

### Choosing Enough Subnet and Host Bits

This requires an idea of how many subnets are required and how many hosts or subnets you will need. 

### DESIGN EXAMPLE

Let’s design 172.16.0.0 with 200 subnets and 200 hosts. 

For 200 subnets, you need 8 subnet bits. Because 2^7 isn’t enough due to it being less than 200. 

Similarly for the host, you also need 8 bits because 2^8-2 = 254, while 2^7-2 = 126.

Since there are 32 bits in the mask, 8 are for subnets and 8 are for the host, then the remaining 16 must be reserved for the network.

This is, therefore a Class B network. 

### Masks and Mask Formats

The subnet mask is 32 bits defined with 1s and 0s.

For example, the subnet mask we just made would be:

```jsx
11111111 11111111 11111111 00000000
```

### Build a List of All Subnets

Subnets reserve subnet numbers and broadcast addresses which cannot be used by hosts. 

Subnet numbers identify the subnet. Subnet broadcast addresses communicate with the hosts in the subnet. 

IP addresses range between the pairs of subnet numbers and subnet broadcast addresses.