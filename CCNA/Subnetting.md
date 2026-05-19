https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE

Subnetting is the process of taking a single network and breaking it up into smaller networks. 

7 Attributes of Subnetting:
- Number of IP Addresses - Number of IPs a Subnet
- CIDR/Subnet - Shorthand notation that tells the size of a network is CIDR (/25, /26)
- Network ID - First possible IP in a subnet; This is how the subnet is referred to. 
- Broadcast IP - Last Possible IP in a subnet; Sending packets here lets you talk to all IPs on the subnet
- First host IP - first usable IP after Network ID
- Last host IP - last usable IP before the broadcast IP
- Next Network - Network ID of the following subnet. (always the IP after the broadcast IP)


**Subnetting Cheatsheet**

Start with 1 on the right, double until you reach 128
In the next row, subtract the first rows value from 256
Finally, write the CIDRs for each column

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   | Group Size   |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ |
| 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 | Subnet Mask  |
| /25 | /26 | /27 | /28 | /29 | /30 | /31 | /32 | CIDR         |
| /17 | /18 | /19 | /20 | /21 | /22 | /23 | /24 | Octet 3 CIDR |
| /9  | /10 | /11 | /12 | /13 | /14 | /15 | /16 | Octet 2 CIDR |
| /1  | /2  | /3  | /4  | /5  | /6  | /7  | /8  | Octet 1 CIDR |


[[Example Problem 1]] 
[[Example Problem 2]]
[[Example Problem 3]]
[[Example Problem 4]]
[[Example Problem 5]]
[[Example Problem 6]]
[[Example Problem 7]]
[[Example Problem 8]]

Speed Tips: 
Sometimes it takes a long time to list out all the possible IPs based on group size. 
You can take shortcuts like multiplying the group number by 10, 20, or 30 and starting from there.
You can also just start from .128, because all of the group sizes are a multiple of this. 
Remember that group sizes will always be a multiple of the subnet values to its left on the table. 

More problems at https://subnetipv4.com/