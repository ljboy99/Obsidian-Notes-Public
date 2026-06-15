**Configuring IPv4 Addresses and Static Routes**

IP Routing sends IP packets from host to destination. It relies on several types of data-links.

**IPv4 Routing Process Reference**

If a destination is local, it will be sent directly to destination MAC address.
If not local, it will be sent to default gateway and forward to the MAC learned by the ARP.

Routers follow a 5 step process to routing packets:

1. If data-link frame haws no errors on FCS, it will be processed
2. Packet will be de-encapsulated
3. Router will decide a route, identify outgoing interface and the next-hop router. 
4. Packet will be re-encapsulated with new header and trailer
5. Frame will be transmitted according to the IP route.

**Example**

Host A: 172.16.1.9 /24
Host B: 172.16.2.9

Host B is outside of Host A's subnet (172.16.1.0 - 172.16.1.255), so the packet will be send to the default gateway 172.16.1.1 after being encapsulated. 

*Routing Step 1: Decide whether to process the incoming frame*
Upon receiving frames, routers will check the FCS field for errors. If there are errors, the frame will be discarded.
It also checks destination address to see if the router was meant to receive that frame; Switches sometimes flood out frames when they don't know exactly where to send to. 

*Routing Step 2: De-Encapsulation of the IP Packet*
The router will now discard the data-link header and trailer. 

*Routing Step 3: Choosing where to Forward the Packet*
The router will now consult the IP routing table looking at the facts of all available routes. 
The router will compare the destination IP with addresses defined in each subnet and match the destination to a subnet. 
This subnet will help the router know where to send the packet out to. 

*Routing Step 4: Encapsulating the Packet in a New Frame*
We now know where the packet will be going.
Now the router must re-encapsulate the frame with a new destination MAC address. 
That new MAC should either have already be learned, or will now be learned via ARP.

*Routing Step 5: Transmit the frame*
The router will now transmit the frame as soon as it can. 