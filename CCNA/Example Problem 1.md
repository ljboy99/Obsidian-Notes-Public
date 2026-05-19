
10.1.1.55 /28

Look at the table. /28 has a mask of 240 so the subnet mask is:

255.255.255.240

Now look at the group size: 16. This tells you how many IPs there are also. 
Note that if you're seeking the number of USABLE addresses, you will subtract 2. In this case that would be 14. 

When you list out increments of possible IPs by 16 starting from zero, you get the following:
.0
.16
.32
.48
.64
and so on. 

.55 is between .48 and .64.
The first number, .48, gives us your Network ID:
10.1.1.48
The other number is the start of the next network:
10.1.1.64
Logically, the address before that is our current networks broadcast IP:
10.1.1.63
With the network ID and broadcast IP, you can get the first and last usable IPs.
First is Network ID +1:
10.1.1.49
Last is Broadcast IP -1:
10.1.1.62

