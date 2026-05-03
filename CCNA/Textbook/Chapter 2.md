Many modern [[router|routers]] and [[Switch|switches]] are bundled together as a single device. These bundled devices are still mainly referred to as routers.

Wireless LANs use radio wages to send bits from node to node.

### [[Ethernet]]

Ethernet is a family of LAN standards defining physical and data-link layers of LAN technology.

Ethernet cables are usually made up of either copper UTP cables or glass fiber optic cabling.

The formal IEEE names for different ethernet cables are prefixed by “802.3” followed by different letters

| Title            | Speed     | Formal Name | Conductor |
| ---------------- | --------- | ----------- | --------- |
| Ethernet         | 10 mbps   | 802.3       | Copper    |
| Fast Ethernet    | 100 mbps  | 802.3u      | Copper    |
| Gigabit Ethernet | 1000 mbps | 802.3z      | Fiber     |
| Gigabit Ethernet | 1000 mbps | 802.3ab     | Copper    |
| 10 Gig Ethernet  | 10 Gbps   | 802.3an     | Copper    |

Ethernet maintains the same data link standard across all it’s different types. The headers and footers maintain the same format no matter the transfer speed.

Ethernet data-link protocols sends “Ethernet Frames” to Ethernet nodes.

These contain sets of data with their headers and trailer.

### Building Physical Ethernet LANs with UTP

Understanding how Ethernet sends data means understanding electrical circuits and how to make signals communicate 1’s and 0’s.

An individual pair in a UTP cable will create a circuit. This is because when both sides are connected to ports, electricity can flow in a continuous loop.

When connected, two devices will use an “encoding scheme” to communicate. This very commonly involves changing voltage at certain frequencies over time.

Ethernet link - Any cable between 2 Ethernet nodes.

Each wire pair in a UTP cable is color coded. For example, a blue pair will have one solid blue wire with a mate that has blue and white stripes.

The ends of these wires will line up with the 8-pins of the RJ-45 connector port.

Once the wires are physically connected with the pins, electricity can flow.

When buying a switch, think about the mix of ports you may need. Often times, you can later on switch ports out for different ones if your configuration has to change drastically.

### Transceivers

Gigabit Ethernet Interface Converter (GBIC) - the original form factors for transceivers.

Small Form-Factor Pluggable (SFP) - smaller replacement for GBIC used with gigabit interfaces.

Small Form-Factor Pluggable Plus (SFP+) - same size port as SFP, but is made for 10 Gig interfaces.

### Cable Pinouts

Straight-Through Cable Pinout

Ethernet NIC Transmitters use pins 1 & 2, while their receivers use pins 3 & 6.

LAN switches have receivers on pins 1 & 2, and transmitters on 3 & 6. This configuration is opposite to NIC Ethernet Devices.

The straight-through cable pinout convention makes this work by connecting pin 1 on one side to pin 1 on the other, pin 2 to pin 2 and so on. This configuration will not work on devices that send data on the same pins and receive data on the same pins. for this, you will need a crossover cable.

A crossover cable will connect pin 1 to pin 3, pin 2 to pin 6, and vice versa, so that the transmitters will be connected to the receivers.

Incorrect cables configurations used to be a wide issue in the industry. This was eventually corrected by the development of auto-MDIX in 1998. Auto-MDIX allows a device to detect whether it’s electrical output is making it to the intended destination, and redirect that output to different pins if it isnt.

### Gigabit Ethernet

1000BASE-T or Gigabit Ethernet uses four wire pairs in it’s UTP, as opposed to the usual 2 pairs in 10BASE-T or 100BASE-T.

The pins of Gigabit Ethernet can all do both receiving and transmitting. They are not hardwired to one role or the other.

Gigabit Ethernet also adds the use of pins 4, 5, 7, and 8, giving electrical currents 8 total paths to move across.

### Fiber Cabling Transmission Concepts

Fiber-optics transfers information by sending light through glass.

The glass core and its classing are shielded by 3 additional outer layers.

In Multi-Mode Fiber, light is received by an optical transmitted and stays in the cables core by bouncing off of the inner cladding until it reaches a receiver. This mode allows the light to enter and bounce from multiple angles. It is less costly than single-mode fiber.

Single-Mode Fiber allows light to travel a straighter path by using an 80% smaller core. Single mode fiber can cover much longer distances than multi-mode fiber, up to 10 kilometers.

Depending on your project, site and needs there are a number of different factors to keep in mind when choosing a type of cable to use on an Ethernet installation.

### Ethernet Data-Link Protocols

Ethernet Frame - composed of an Ethernet header at the front, encapsulated data in the middle and an Ethernet trailer at the end.

### Ethernet Addressing

When sending a frame, the source node will put its address in the source field, and destination address in it’s destination field.

Most computers are represented by an Ethernet address/MAC address. This is a 12 digit hex number to identify the device by.

To avoid confusion, manufacturers must have their products be assigned a unique 3-byte prefix by the IEEE. This is an organizationally unique identifier / OUI. Manufacturers must give all devices under a single OUI a unique 3-byte suffic at the end of their MAC address.

**Group addresses** identify more than one LAN interface card. This can be used to send frames to multiple devices.

**Broadcast address -** frames sent here are delivered to all devices on a LAN

**Multicast address -** Copies and forwards received data to a specific set of devices.

The “Ethernet Type Field” or EtherType helps netowrk processing on routers and hosts.

### Error Detection with FCS

Ethernet Frame Check Sequence lets a receiving device compare its data frame with what the sending device transmitted to it by using a formula that they both share.

If the results that the sender and receiver get after using the formula are differet, then it tells the devices that there has been an error.

### Full and Half Duplex Logic in an Ethernet LAN

Half duplex logic states that if a device is receiving an Ethernet frame, other devices must wait until the Ethernet is not being used before sending anything else.

Full Duplex logic states that adevices on a LAN can freely send and receive Ethernet frames at the same time.

Most, if not all, modern PCs and LAN switches run with Full Duplex logic.

Older LAN hubs use Half Duplex logic. This is because if a hub were to send and receive data at the same time, it would cause a data collision.

To avoid collisions, half duplex logic makes data wait until the sender sees that the ethernet is not currently busy.

Errors can still occur sometimes, for example if two senders see that the ether net is not currently, busy and decide at the same time that it’s a good time to send data, it may cause a data collision.
