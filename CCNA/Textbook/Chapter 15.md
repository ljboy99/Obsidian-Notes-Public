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

**Choosing The Best Mask**
Decisions on what mask to use may be based off of:
- Number of hosts per subnet
- Number of subnets
- Number of supported subnets and hosts

Example:
If your mask range is /22 - /24:
- /22 has the least subnet bits and the most host bits
- /24 has the least host bits and the most subnet bits
- /23 is right in between and allows growth for both sides. 

**The Formal Process For Selecting a Mask**
1. Find the amount of network bits per class rules: 
	1. Class A - 8 bits
	2. Class B - 16 Bits
	3. Class C - 32 Bits
2. Calculate the minimum subnet bits so that 2^S => required amount of hosts per subnet
3. Calculate the minimum host bits so that 2^H - 2 => the required amount of hosts per subnet
4. If N + S + H > 32, There will be no mask that works.
5. If N + S + H = 32, 1 mask will work.
	1. Calculate /P as P = N + S
6. If N + S + H < 32, Multiple masks can work.
	1. Calculate /P on the minimum value of S, where P = N + S. This is the maximum number of hosts per subnet.
	2. Calculate /P on minimum value of H, where P = 32 - H .This maximizes the number of possible subnets. 

**Finding All Subnet IDs**
First Subnet ID: The Zero Subnet
The Zero Subnet is the first subnet ID which ends in zero. 
For example, for network 172.20.0.0, the zero subnet is 172.20.0.0.
The zero subnet is called the zero subnet because in binary, it's zero part is all zero's.

Engineers tend to avoid using the Zero Subnet due to the confusion that can be caused by using a subnet which is identical to the network ID. 
This also used to cause issues with older hardware that didn't distinguish between the Zero Subnet and the Network ID. 

**Finding the Pattern by Using The Magic Number**
The 'Magic Number' is 256 minus the decimal value of the 'Interesting Octet'
The Interesting Octet is the Mask Octet which does not have a value of 255.

For example, let's look at 255.255.254.0
256 - 254 = 32.
So the pattern for this mask will be:
0 --- 32 --- 64 --- 96 --- 128 --- 160 --- 192 --- 224 --- (256)
Remember that 256 is not really included because you can't make a valid IP or mask with it. 

**A Formal Process of Finding Patterns When There are Less Than 8 Subnet Bits**
1. Write out the Subnet Mask
2. Identify the Interesting Octet
3. Calculate the magic number by subtracting the interesting octet's value from 256.
4. Write out the classful network number (Same as the zero subnet)
5. STEP 5
	1. Copy over the uninteresting octet values
	2. add the magic number to the previous interesting octet
6. Keep listing these masks. Once you are about to reach 256, the last subnet before you would've wrote 256 is the broadcast subnet. 

**Example**
STEP 1:
Network: 172.16.0.0
Mask: 255.255.240.0

STEP 2: In the mask, octet 3 (240) is the interesting Octet
STEP 3: 256-240 = 16
STEP 4: The zero subnet is 172.16.0.0
STEP 5-6:
176.16.0.0
176.16.16.0
176.16.32.0
176.16.48.0
...
...
...
176.16.224.0
176.16.240.0
XXX.XX.256.X

Broadcast Subnet is 176.16.240.0

**Finding All Subnets with Exactly 8 Subnet Bits**
There's only exactly 8 subnet bits when: 
- You're on a Class A network with the mask 255.255.0.0; the entire second octet has subnet bits.
- Or you're on a Class B network with the mask 255.255.255.0; the third octet has subnet bits. 

Because what usually is the interesting octet is instead "255", the magic number will always be 1. Because 256-255 = 1

So, when you're finding all the possible IP's, you will iterate by 1.
Ex.
172.16.0.0
172.16.1.0
172.16.2.0

And so on. 

**Finding All Subnets with More Than 8 Subnet Bits**

If there's 9-16 subnet bits:

When there's more than 8 subnet bits, your subnet field will be more than one octet, usually with one interesting octet, and octet with 255 to the left. 

**Example**
Network: 130.4.0.0
Subnet: 255.255.255.192

List the subnets:
130.4.0.0
130.4.0.64
130.4.0.128
...

Once you get to the end of the last octet, where you would otherwise be at 256, here you will add 1 to the just-left octet, and start back from zero:
130.4.1.0
130.4.1.64
130.4.1.128
130.4.1.192
130.4.2.0
130.4.2.64
...

You'll notice that you have 4 different subnets for every time you add to the just-left.
Also understand that, here, you will have 10 subnet bits. This is because you have a Class B network with 16 bits, and your subnet prefix adds up to /26. 26 - 16 = 10.

This tells us you'll have 1024 subnets because 2^10 = 1024. 

-------

Now the process if your network has 17+ subnet bits is similar. You will just have another octet to the left with an increment of 1, so once your first just-left octet hits 256, then it turns into 0 and the next left will increase by 1. 

Think of this like a really big abacus with 256 beads on each rod.