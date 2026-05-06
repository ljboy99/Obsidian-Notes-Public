## Defining a Subnet

Rules for choosing subnet addresses:

- Contains consecutive numbers
- holds 2^H numbers
- Lowest number is Subnet ID
- Highest number is broadcast address
- All other addresses are unicast IP addresses

## Subnet ID Concepts

Subnet ID represents a subnet.

The subnet ID is usually recorded by routers that find a subnet in the network.

It is the first and smallest number in the subnet.

## Subnet Broadcast Address

It’s a destination to send packets across the entire subnet. 

Identifies high end of addresses in a subnet.

As a broadcast, if a subnet sends data to a subnet broadcast address, the host of that address will broadcast it to all hosts in the subnet. 

## Range of Usable Addresses

Before leasing and reserving addresses, you should know what’s usable.

The first usable is (subnet ID + 1)

Last usable is (Broadcast address - 1)

See the example below

| Subnet ID | 172.16.128.0 |
| --- | --- |
| First Usable  | 172.16.128.1 |
| Broadcast | 172.16.128.255 |
| Last Usable | 172.16.128.254 |

## Analyzing Existing Subnets - Binary

- All numbers in a subnet share the same prefix
- Subnet ID is lowest values so host part is all 0 in binary

Example

127.16.150.41 - Mask /18

/18:

PPPPPPPP PPPPPPPP PP|HHHHHH HHHHHHHH

172.16.150.41:

10101100 00010000 10|010110 00101001

Subnet ID:

10101100 0001000 10|000000 00000000

The Subnet ID is 172.16.128.0 becuase you change all of the host bits to 0.

## Finding the Subnet Broadcast Address in Binary.

The process is similar except you would change the host bits into 1 instead of 0.

So for the last example the broadcast in binary would be:

10101100 00010000 10111111 11111111

Which is 172.16.191.255

## Shortcut for the Binary Process

Remember any parts where the octet part is 255 will have the same IP part in the end.

Any parts where the subnet is 0 will end up as 0 for that part of the subnet or as 255 for the broadcast address. 

## Analyzing Existing Subnets in Decimal

Any octets with 255, you copy the starting decimal IP.

Any with 0, you will write 0 in pace of what the starting IP had if you’re finding the IP, and 255 if you’re finding the broadcast address. 

Example

| IP | Mask | ID | Broadcast |
| --- | --- | --- | --- |
| 10.77.55.3 | 255.255.255.0 | 10.77.55.0 | 10.77.55.255 |
| 172.30.99.4 | 255.255.255.0 | 172.30.99.0 | 172.30.99.255 |
| 1.95.53.76 | 255.0.0.0 | 1.0.0.0 | 1.255.255.255 |

## Predictability in the Interesting Octet

The interesting octet is the octet which is neither 0 or 255.

Depending on the mask, the subnet will be a multiple of a certain number

| Mask | Multiple of |
| --- | --- |
| 255.255.128.0 | 128 |
| 255.255.142.0 | 64 |
| 255.255.224.0 | 32 |
| 255.255.240.0 | 16 |

## Finding the Subnet ID: Difficult Masks

If an octet is neither 0 or 255 for a subnet:

Calculate 256 - mask (magic number)

ID will be a multiple of that number closest to the IP without going over. 

Example:

IP - 130.4.102.1, Mask - 255.255.240.0

| 255 | 255 | 240 | 0 |
| --- | --- | --- | --- |
| 130 | 4 | 102 | 1 |

256 - 240 = 16

102/16 = 6R6

16 * 6 = 96

Subnet ID: 130.4.96.0

## Finding Broadcast Addresses for Difficult Masks

If a mask is neither 255 or 0:

Magic number = 256 - mask

(Subnet ID value + magic number) - 1

Example:

IP - 130.4.102.1, Mask - 255.255.240.0

| 255 | 255 | 240 | 0 |
| --- | --- | --- | --- |
| 130 | 4 | 96 | 1 |

256 - 240 = 16

96+16-1 = 111

Broadcast address is 130.4.111.255