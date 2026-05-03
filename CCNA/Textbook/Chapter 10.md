## Understanding RSTP Through Configuration

Cisco switches come with RSTP enabled

The need for multiple spanning trees was created by the emergence of VLANs

The only part of the Bridge ID you can manually configure is the priority.

Priority is set in a multiple of 4096. This is selected by the first four digits in a 16 digit binary sequence.

For example, 4096 would be symbolized as 0001 0000 0000 0000

Cisco switches have a default priotity of 32,768. Engineers will adjust this number to set roots and create specific arrangements for their networks.

## Identifying Switch Priority and Root Switch

The latter 12 digits after the priority (first 4) is the System ID Extension

Ex. 1000 (0000 0000 1001)

## Identifying Root

To arrange networks and achieve desired STP goals, some switches will be reconfigured to be lower than base priority, because the lowest priority is root. See the following command.

```jsx
# show spanning-tree vlan #
```

This command will give you informaition about the Root’s Bridge Id, and the current switches BID. If the current BID matches the root BID, that means you are on the Root Switch.

## Switch Priority Using Root Primary and Secondary

To configure the two switches to be most likely be root, use the following commands.

```jsx
#spanning-tree vlan # root primarty
	######## NOW ON ANOTHER SWITCH USE FOLLOWING COMMAND
#spanning-tree vlan root secondary
```

The command performed on the first switch, the primary, will set the priority to either 24,576 OR 4096 less than the lowest switch if there are other switches lower than default.

The second command sets the priority of a switch to be 28672, because this is less than the default, and more than what the primary is usually set to.

## The Differences between RSTP and RPVST+

|RSTP|RPVST+|
|---|---|
|Create a ‘common’ STP tree|Creates a tree for each VLAN|
|Sends one BPDU set for the entnire network|Sends one set of BPDUs per VLAN|
|Sends to IEEE standard multicast address: 0180.C200.0000|Sends to Cisco proprietary multicast address: 0100.0CCC.CCCD|
|On trunks, BPDUs are sent without a VLAN header|On trunks, BPDUs are sent with headers for the VLANs they came from|
|Sets BID VLAN field to 0000.0000.0000|Sets BID VLAN field to the VLAN ID|
|Basically doesn’t account for the existence of VLANs in general.||

## Identifying Port Cost, Roles, States.

The “show spanning-tree vlan #” command will detail port roles, costs and states.

You can changee port roles by declaring port costs in the CLI config mode.

Ex. # spanning tree vlan 9 cost 10

## Optional Features

PortFast is enabled with

```jsx
#spanning-tree portfast
```

This only works on access ports, and will not make changees in a trunking system.

BPDU Guard is enabled by:

```jsx
#spanning-tree bpduguard enable
```

This will enable BPDU Guard whether or not trunking or portfast is present.

Once it’s enabled, if any BPDU is received, BPDU Guard puts the receiving port in an error-disabled state and removed the device from STP topology.

The interface can be reset by sending a shutdown command followed by a no shutdown command.

## PortFast on VLAN Trunks and Voice Psuedo-Trunks

You should not use PortFast with ports on a trunk connected to other switches, but use it on ports connected to endpoints or IP phones.

The following command will enable PortFast on voice VLANs

```jsx
# switchport voice vlan #
```

Sometimes you will need to check if IOS actually applied Portfast using the following command.

```jsx
#show spanning-tree
```

Any ports that show ‘p2p edge’ in the resulting table are using portfast. Ports that just say ‘p2p’ do not use portfast.

## Global Configuration of PortFast and BPDU Guard

You can enable these features on an entire switch with the following commands in sequence.

```jsx
# spanning-tree portfast default
# spanning-tree portfast bpduguard default
```

This enables PortFast on all access ports and then enables BDPU Guard on all the PortFast Ports.

### Conditional BPDU Filtering with Global Configuration

Default setting is

```jsx
#no spanning-tree portfast bpdufilter enable
```

This is reversed with

```jsx
#spanning-tree portfast bpdufilter enable
```

This will enable the BPDU filter on PortFast ports.

If you want to see all the interfaces in the VLAN:

```jsx
#show spanning-tree
```

Remember that after a set time of not getting a response from a BDPU Guard port, the other interface should stop sending BDPUs.

### Disabling STP w/ BPDU Filter Interface Configuration

BPDU Filter also filters outgoing BPDUs, effectively taking that port out of STP

Be careful with enabling BPDU Filter, because it can cause forwarding loops that can disable an entire LAN

If you were to show the status of the interface port with BPDU Filter, it would show 0 sent and received BPDUs.

### Root Guard

Root Guard should only be used on ports connected to other switches as well as switches that should not be receiving BPDUs from superior switches.

This is because Root Guard will disable ports that receive those superior BPDUs as a mean to protect the root status of that switch. Switches with Root Guard that receive superior BPDUs will be put into a ‘broken status’ and discard all following BPDUs on that port.

### Configuring Layer 2 EtherChannel

An EtherChannel is a set of parallel links that switches can treat as a single link.

An EtherChannel lets switches use all available links that would otherwise be blocked by STP or RSTP.

EtherChannels can also be referred to as a PortChannel or a channel-group

Manual EtherChannel configuration is done by adding all ports to the correct ‘Channel-group’ with the ‘on’ keyword and a channel number.

The command will look something like:

```jsx
#channel-group 1 mode on
```

Using an EtherChannel will combine the bandwidth of the links.

So if your channel has 2 links that are 1 GBPS each, you will show as having a bandwidth of 2 GBPS

### Configuring Dynamic EtherChannels

Switches can be enabled to dynamically send messages to see if links have certain qualifications and add them to the EtherChannel if they pass checks for those qualifications.

|Cisco-Proprietary Port Aggregation Protocol (PAgP)|Link Aggregation Control Protocol (LACP)|
|---|---|
|Supports 8 total links|Supports 16 total links, with 8 active at a time|
|Uses the terms ‘desirable’ and ‘auto’|Uses the terms ‘active’ and ‘passive’|
|At least one side must be desirable for negotiation to happen.|At least one side must be active for negotiation to happen.|

### Interface Configuration Consistency with EtherChannels

When changes are made to a port in an EtherChannel it will be compared to other ports. If it doesn’t match the others, it will not be used, and will be set to a ‘non-working’ state.

The switch will check a port for: Speed, Duplex, Access/Trunk state, VLAN, VLAN list and Native VLAN

Once you make changes and the switch makes it’s comparisons, it will declare in the logs if the port is now incompatible.

If you use “#show etherchannel port-channel”, it will show statuses including active ports and how long since a port was bundled or unbundled.

### EtherChannel Load Distribution

Etherchannels will make a switch associate MAC addresses with port channels instead of physical ports.

Once that frame must be sent out, the switch needs to decide which port in the port-channel to use. Those decisions will be based on the values found in the layer 2, 3 and 4 headers.

Load distribution is enabled with the following command.

```jsx
#port-channel load-balance
```

There are different load distribution algorithms but many of them have some common goals. This includes:

- Send all messages over a single link in order.
- Utilize all links in the EtherChannel
- Balance traffic across active links
- Make sure not to reorder the messages.
- Send messages for an app link over the same app link by using the information in the headers.

With these goals in mind, different load distribution methods will use different ways to move frames.