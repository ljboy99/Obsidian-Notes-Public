The Dynamic Host Configuration Protocol Server 

Clients will ask for network parameters from the DHCP Server

The DHCP Server will provide clients with: 
- IP Address
- Subnet Mask
- Default Gateway
- Domain Name
- DNS Server

The process is as follows: 
1. Client sends broadcast packet to find DHCP servers
2. Server receives packet and sends "DHCP Offer" with IP info
3. Client accepts the first DHCP Offer by sending DHCP Request for needed parameters
4. DHCP server approves with an Acknowledgement packet with duration and configuration information.

