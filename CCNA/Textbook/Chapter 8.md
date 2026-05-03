# Implementing Ethernet Virtual LANs

## Virtual LAN Topics

A LAN includes all devices in the same broadcast domain

When a broadcast frame is received by a switch, it gets sent to all the interfaces on that LAN.

To avoid having buy a whole new switch to make a separate LAN, interfaces on a single switchs can be separated into different VLANs, which can be a more efficient target for broadcast frames.

VLANs also reduce the overall CPU load, improves security, reduces STP workload, and can be used to separate people’s devices into groups based on their role as opposed to their location. 

## Creating Multiswitch VLANs with Trunking

Trunking adds a VLAN header to ethernet segments, to tell the frame what VLAN it is traversing/where it belongs.

Without trunking, VLANs would require wired connections between eachother, which does not scale well. 

### VLAN Tagging Concepts

Trunking links switches together while keeping different VLANs separate. 

Trunking adds a header to Ethernet frames to tell it what VLAN to go to as it moves between switches. 

It lets switch 1 tell switch 2 what VLAN the frame belongs to.

Switch 2 sees the target VLAN during the deencapsulation process. 

### 802.1Q & ISL VLAN Trunking Protocols

Cisco used their inter-switch link protocol (ISL) until the IEEE released 802.1Q protocols. 

802.1Q fills the same role of tagging frames with a VLAN ID, but adds an extra 4-bit VLAN header.

There are 2 ranges of VLAN ID numbers

Normal range = 1 - 1005

Extended range = 1006-4094

802.1Q also utilizes a “Native VLAN”.

The Native VLAN is used for improper configurations, where headerless frames would otherwise be discarded. 

## The Need for Routing Between VLANs

Layer 2 logic (receiving ethernet frames, looking at MAC, forwarding frames) happens within (but not between) VLANs.

VLANs function interact as if they were two separate switches. This keeps VLAN traffic separated.

## Routing Packets Between VLANs with a Router.

Devices in a VLAN should exist in the same subnet. These should be separate from other subnets. 

Because they are separate, you need a device to act as a router between VLANs. Some (not all) switches have capabilities built in to fill this role. 

## Creating VLANs and Assigning Access VLANs to an Interface.

To configure a new VLAN:

From global configuration mode create a vlan and move into vlan configuration mode with the following commands:

```jsx
switchname>enable
switchname#conf t
switchname(config)#vlan 1
swithcname(config-vlan)#name myvlan
```

As you can see, you may also assign a name to your vlan.

For each access interface:

Move to interface configuration mode with:

```jsx
switchname# interface (type) (number)
```

The parentheses here denote values that you will fill in with your own information. 

Proceed to associate the interface with a vlan, for example VLAN 1

```jsx
switchname# switchport access vlan 1
```

Set the port to operate in access mode, as opposed to trunking mode:

```jsx
swtichname# switchport mode access
```

You can also add a range of ports to a VLAN in one group of commands. Note that any VLANs that don’t exist in your specified range will be created on the spot. Here we will assign ports 15 and 16 to VLAN 3:

```jsx
switchname# interface range FastEthernet 0/15-16
switchname# switchport access vlan 3
```

## VLAN Trunking Configuration

```jsx
swtichname# switchport mode trunk
```

Trunking can be enabled by simply entering a command on each side of the established link.

Trunking can be further configured to change what type of trunking occurs, or when you want to trunk. 

For switches that support both ISL and 802.1Q, encapsulation or Dynamic Trunking Protocol will help determine what type of trunking to use. 

Administrative mode configuration determines whether trunking will be used at all. 

Operational mode will tell you whether an interface is a trunk or an access port. 

## Implementing Interfaces Connected to Phones

IP Telephony is a networking branch where phones use IP packets to send and receive voice transmission. It utilizes Ethernet as opposed to older phone/voice switch connections. This enables phones to communicate over an IP network. 

To lower costs, modern Cisco phones have a built in LAN switch.

Cisco recommends IP phones to be sorted into a VLAN that is separated from PCs. This results in a Data VLAN and a Voice VLAN.

### Data and Voice VLAN Configuration and Verification

You’ll configure the VLANS by selecting a range, changing the switchport to access mode, and defining the voice ports.

```jsx
switchname#switchport voice vlan 11
```

Now if you show the interface that the voice vlan is assigned to in the CLI, it will show what voice VLAN that port is on.

```jsx
switchname> show interfaces FastEthernet 0/4 switchport
```

*This examples assume we assigned the port to Fa0/4.*

That command will show what Voice VLAN the specified port is associated with.

If you want to see what VLANs are allowed on an interface trunk, you will use the following command

```jsx
switchname#show interfaces F0/4 trunk
```

## Troubleshooting VLANs and VLAN Trunks

**Step 1: Confirm The Correct Access VLAN is Assigned**

```jsx
show vlan
show vlan brief
```

Use one of those two prior commands to confirm the VLAN access status.

Identify ports with the “show vlan id ____” command

**Step 2: Confirm The Access VLAN is Defined and/or Active**

Frames will not be forwarded if the VLAN is unknown or not active.

Try defining the VLAN you’re having issues with in the console.

You can use the “show vlan” command to see if the VLAN you’re working on is active or in shutdown status.

When you use the “show vlan” command, any disabled known VLANs will show up as “act/lshut”.

**Step 3: Check if Access is Undefined or Disabled**

Remember VLAN are defined either manually, or by switches learning from other switches. 

If you find that a target VLAN does not exist in the system, see if anything changes when you manually configure it.

Remember that VLANs are disabled with the “shutdown” command and enabled with the “no shutdown” command/ 

**Step 4: Check for Mismatched Trunking Operational States**

A common mistake that will cause a misconfiguration on a machine is a result of the use of the following command:

```jsx
#switchport mode dynamic auto
```

This will cause the machine to wait for the other end of the link to initiate negotiations. Obviously, if both sides are waiting, there will be no negotiation.

You may also have a link where one side is configured to trunk, and then other is not. No trunking will take place in this kind of config. 

This configuration can cause a lot of confusion, because it will show an up/up status, but will block traffic on the VLAN. 

Step 5: Check your Supported VLAN List.

```jsx
#show interfaces **INTERFACE-ID** trunk
```

Replacing the underlined with an actual interface ID, this command will show which VLANs traffic will be forwarded over the trunk. 

If a VLAN shows up in the output of this command, the following is true:

The VLAN has not been removed from the allowed VLAN list.

The VLAN is active on the local switch

The VLAN has not been VTP pruned

Network engineers can define a limited list of what VLANs are allowed on a trunk. This is done with the following command:

```jsx
#switchport trunk allowed vlan 1-50
```

This command will allow trunking on VLANs 1-50. This range of 1-50 can be replaced with any valid range of VLANs on your network. 

See the following command:

```jsx
#show interfaces trunk
```

This will show you 3 lists:

1. The allowed VLANs on the trunk.
2. Currently active VLANs.
3. VLANs that are in STP forwarding mode and not pruned.