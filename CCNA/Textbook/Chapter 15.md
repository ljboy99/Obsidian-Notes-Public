Subnet Design

**Choosing the Minimum Number of Subnet and Host Bits**
Networks must be designed with the required number of subnet and host bits in mind. 
You need to be able to uniquely number each subnet and host.
It's useful to keep a table of the powers of 2 until you memorize them

Initial steps to choose a mask:
1. Determine number of network bits (N)
2. Determine smallest possible value of S, so 2^S is greater than required number of subnets
3. Determine the smallest possible value of H so that 2^H - 2 is greater than the required amount of hosts per subnet.

Sometimes the required amount of subnets and hosts may exceed 32 bits. In this case, there is no mask that meets the requirements.
For example, if s=9 and h=9, a class B network with 16 network bits wil not work because 16+9+9 = 34.

**One Mask Meets Requirements**
If the smallest number of host bits, smallest number of subnet bits and network part add up to 32, exactly one mask meets the requirements.

**Multiple Masks Meet Requirements**
Start by finding out all of the masks that could be applied.
1. Calculate shortest /P based on minimum value of S in P=N+S
2. Calculate longest /P based on minimum H in P=32-H 
3. The valid mask range is all masks between the results of steps one and two. 