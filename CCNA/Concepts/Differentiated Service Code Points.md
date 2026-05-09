DSCP manages and prioritizes packets by attribute based on a **6-bit** value in the IP header.  

The benefit is that you can control the priorities of data. It also optimizes the network by allowing the dropping of specified packets.

There are 3 major DCSP markings:

Expedited Forwarding (EF):
Known as DSCP 46 because in binary it is 101110. It's used for Voip, streaming and gaming.

Assured Forwarding (AF) Classes:
AF packets have different priorities with different "drop precedences", which dictate how likely a packet will be to be dropped if there is a conflict. It's 1-4, with drop precedence one being the lowest possibility of being dropped.

Best Effort (BE):
Used for data without specific prioritization. These are last priority. 