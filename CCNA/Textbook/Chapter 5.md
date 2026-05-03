## LAN Switching Concepts

Campus LAN - Network connecting end users to switches that provide connections to the server side, and to the rest of the network.

“Data Centers” usually contain the switches and servers that are connected to each other. 

## Overview of Switching Logic

Main goal of a LAN switch is to forward frames to a destination mac address.

Once receiving a frame, a switch will either forward or ignore

Switches perform three actions to achieve their main goal:

1. Decide when and when not to forward frames based on the MAC destination.
2. Learn source MACs to prepare for forwarding future frames.
3. Achieve STP by working with all switches to create an endless loop of frames. 

## Forwarding Known Unicast Frames

Switches reference a table of MAC addresses to help decide whether frames should be forwarded and where to.

This table can go by a few different names:

- MAC Address Tables
- Switching table
- Bridging table
- CAM Table
- Content Addressable Memory Table.

## Learning MAC Addresses

Another function of switches is to create a table of MAC addresses from the information that it observes

Once a switch receives a frame from a device that it hasnt interacted with before, it will log that devices into its MAC Address Table. 

Once added to the address table, that MAC is now associate d with the port that the switch received the frames from. 

So if a device with a MAC address of 0200.1111.1111 sends a packet to port F0/1 on the switch , that is the port that it will be paired up with on the MAC Address Table. 

## Flooding Unknown Unicast and Broadcast Frames

If a switch receives a frame but does not have the destination MAC already in it’s address table, the frame is forwarded to all interfaces except for the one that sent it. This process is known as “Flooding”

## Avoiding Loops with Spanning Tree Protocol

Flooding will continuously forward frames until it finds the proper recipient. This can cause an endless loop if that recipient can’t be found. 

STP forces interface to block or forward PDUs. Blocking the correct subset will leave only one possible path between each pair of LANs, which will prevent the clogging of networks. 

## Verifying and Analyzing Ethernet Switching.

Cisco Catalyst switches come prepared to switch frames with their default settings.

The interfaces can work off their default presets and have many functions enabled by default, including MAC learning, flooding, forwarding and STP. 

To see a MAC Address Table in the CLI you will type either of these commands:

```jsx
show mac address-table
show mac address-table dynamic 
```

This will show a table of MAC addresses and correlated ports. 

## MAC Address Table

The table has 4 Column

| VLAN | MAC Address | TYPE | PORTS |
| --- | --- | --- | --- |
| Tells which individual VLAN that the switch will forward or flood packets in.  | The “MAC Address” will be list with the “ports” that the switch associates with them  | Shows how the switch learned about this MAC address, either Static or Dynamic | Shows the port connection associated with a MAC address. Will identify the port type by “Fa” for fast ethernet and “Gi” for Gigabit-ethernet. They will be followed by the correlated port number.  |

## Switch Interfaces

You can check interface status with the following command:

```jsx
show interfaces status
```

This will show you port column and a status column showing whether that port is connected orn not/ 

You may also send commands to look at specific interfaces. Here are examples of those commands

```jsx
show interfaces f0/1 status 
show interfaces f0/1
```

You can also see stats about frames going through interfaces with the “counters” command.

```jsx
show interfaces f0/1 counters
```

## Finding Entries in the MAC Address Table

Because you may work with very large networks, it’s useful to be able to single out interfaces to check their status 

```jsx
show mac address-table dynamic address 0200.1111.1111
```

This will show the single entry for that MAC addresses

You may also want to be able to single out a device by it’s connected port

```jsx
show mac-addresses dynamic interface fastEthernet 0/1
```

Or by VLAN 

```jsx
show mac address-table dynamic vlan 1
```

## Managing the MAC Address Table (Aging, Clearing)

By default, a switch is set to remove a MAC address entry after 300 second s of inactivity from that device. 

This timer resets every time the switch interacts with that interface.

You are also able to change this timer

```jsx
mac address-table aging-time 1000 [vlan 2]
```

Memory is also limited, so when a switch hits maximum capacity, the oldest entries will be deleted to fit the new data.

## MAC Address Tables with Multiple Switches

In an example where two devices each connect to a switch, connected to another switch with the same arrangement, the MAC address table would associate the MAC addresses of the computers on the other switch by the port where it receives data from them on it’s own switch.