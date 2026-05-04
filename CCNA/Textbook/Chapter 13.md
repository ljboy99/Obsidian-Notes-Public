## Analyzing Subnet Masks

Subnet masks are in binary and follow these rules:
No patterned octets (ex. 01010101, 10101010)
1’s are to the left and 0’s are to the right (1111111 11111111 00000000 0000000)

Dotted decimal notation makes it easier for humans to read masks.
Ex. 255.0.0.0 is written in DDN.

Prefix format is a “/” followed by the number of 1’s in the subnet.
Ex. /8, /24
This is also known as a CIDR mask.

## Converting Between Binary and Prefix Masks

This is easy, as prefix is simply a count of the 1’s in the binary mask. 
ex. 11111111 1111111 11110000 00000000 is /20
11111111 00000000 00000000 00000000 is /8

## Converting Between Binary and DDN Masks

This utilizes the math of binary.

From left to right, a 1 represents the presence of any of these numbers:
128, 64, 32, 16, 8, 4, 2, and 1.
So 11110000 would be 240

With the fact that all 1’s are left and all 0’s are right, it’s possible to memorize the 9 values. 

| 00000000 | 0 |
| --- | --- |
| 10000000 | 128 |
| 11000000 | 192 |
| 11100000 | 224 |
| 11110000 | 240 |
| 11111000 | 248 |
| 11111100 | 252 |
| 11111110 | 254 |
| 11111111 | 255 |

## Converting Between Prefix And DDN

Generally, you’ll want to convert from decimal to binary, then binary to prefix, and vice versa.

## Identifying Subnet Design Choices Using Masks

Masks have many roles.

Masks divide the subnets address into two parts.
The mask spits the subnet part from the host part. 
The Prefix, or subnet part, functions like a zip code, showing nodes that belong in the same area. 
The host part identifies unique hosts. 

Ex. A mask of 255.255.255.0 has 24 bits and can be labelled and /24.

## Masks and Class Divide Addresses into 3 Parts

They’re divided into: Network | Subnet | Host.

Network and subnet act like a prefix because they match across the entire subnet.

## Classless and Classful Addressing

Classless Addressing: gives IPv4 2 parts, prefix + host

Classful Addressing: gives IPv4 3 parts, Network + Subnet + Host

The division of these parts will be based on the rules of classes A, B and C.

Whether classless or classful, the bits in an address always add up to 32. 

## Calculations Based on IPv4 Address Format

Find how many hosts in the subnet:

2^H - 2 ; Where H = host bits

Find how many Subnets in network:

2^S ; Where S = subnet bits

## Masks and CIDR Blocks

Instead of working with classes, CIDRs have their own prefix lengths and IDs to use.