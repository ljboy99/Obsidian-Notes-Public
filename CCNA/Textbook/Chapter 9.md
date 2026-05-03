# Spanning Tree Protocol

STP, a precursor to the modern RTSP, lets LANs be designed with redundancy so it continues to function if some links fail. 

Without STP, LANs w/ redundant links would cause Ethernet frames to loop indefinitely. STP enables frames to be delivered to each device without causing endless loops. 

STP checks if a port is in one of two states: forwarding or blocking. 

It does not affect device states, but rather adds an additional one. 

STP also prevents ‘broadcast storms’, where one frame will loop around indefinitely, getting in the way of more productive frames. This is because it causes a congestion which prevents frames from being delivered to their destination. 

In a broadcast storm, the frame will perpetually loop through a LAN system until that chain is broken (like if a node is shut down). 

Broadcast storms can cause “MAC Table Instability”, where the LAN device’s MAC tables keep updating constantly as a result of a looping frame going back and forth from different switches. 

Because in a broadcast storm, the whole network is receiving the same frames, the destination node can receive the frame many times more than expected, causing app failure and network issues. 

Spanning Tree Protocol put all switch ports in either a forwarding state or blocking state.  

A blocking state prevents port from receiving (and therefore resending) frames. This prevents a broadcast storm because no ports will be receiving and repeating frames that aren’t meant for them.

STP spans interfaces out in a single path starting from the Ethernet link. 

STP elects a root switch. All interfaces are forwarding. 

## STP Bring ID and Hello BPDU

Switch are assigned a unique Bridge ID (BID) in 8-bytes based on their MAC

Switches exchange bridge protocol data units (BPDU’s) to send messages. 

The “Hello BPDU” provides other switches the following information:

The senders Bridge ID

The root switch’s Bridge ID

The sender’s root cost

Timer values for MaxAge, Forward Delay, etc. 

## Electing the Root Switch

A root is elected based on Bridge ID’s. The lowest priority BID number becomes the root switch. For example a priority of 4096 would beat out 8192 for root. 

If priorities tie, the next deciding factor is the lowest MAC address. 

In summary, all switches will flood BPDU’s to eachother, claiming that they are the root, until they’re proven otherwise by a lower priority (and MAC if applicable). This process will go on until only one switch is claiming to be the root. 

## Choosing Each Switches Root Port

Other switches need to choose their root port. This is the port they have which has the lowest cost to reach the root switch. 

For example, if switch 3 can pass frames through switch 2 to get to the root, or pass to the root directly, passing frames directly to the root likely has the lowest root cost.

These root ports are figured out by looking at their own root costs, as well as the root costs of their peers to decide what is most efficient. 

If root costs tie, the root ports will then be decided by:

The lowest Bridge ID, 

Lowest port priority,

Lowest port number

## Choosing Designated Port on each LAN Segment

On a link with a switch and a second device that doesn’t use STP, the switch becomes a designated port. 

The Designated port is decided when all interfaces figure out who has the lowest root cost. 

DP’s are put in a forwarding state. 

## Configuring to Influence STP Topology.

STP is enabled by default, and has default configurations on CISCO switches. These configurations, of course, can be changed. 

An engineer may change the priority of a device to make it lowest in a system & win root election. 

Port costs can be altered as need. 

# Details Specific to STP (and not RSTP)

## STP Activity When Network Remains Stable

When a network is idle, the root will ping all branches of the STP with “Hello BPDUs”. All switches receiving the Hello will forward it further down the tree 

This repeats continuously, as once a switch, doesn’t receive an expected “hello”, it knows an issue has occurred. 

## STP Convergence is Managed by 3 Timers

The period between Hello BPDU’s created by root is 2 seconds by default. This can be adjusted. 

MaxAge is 10 times the duration of the Hello timer. This is how long a switch will wait after missing a hello to switch STP topology. 

Forward Delay is the duration that a switch listens and learns when the process from transitioning from blocking to forwarding is affected. The default for this is 15 seconds. 

Once a switch passes it’s MaxAge, the root switch rank is recalculated, and the entire topology may change. 

## Changing Interface States with STP

STP utilizes roles and states. 

Roles help STP analyze LAN topology

States tell switches whether to send or receive frames. 

Roles and states are directly affected by STP convergence.

A switch can instantly go from forwarding to blocking. 

Going from blocking to forwarding, though, requires listening to remove stale MAC entries from it’s table, and learning to update the table.

### Rapid STP Concepts

RSTP shares some traits with standard STP:

They elect root switches, root ports, and designated ports by the same rules.

They put ports in forwarding and blocking states. 

RSTP can work alongside STP

The main improvement that RSTP has over STP is the convergence speed. 

STP convergence will take around 50 seconds.  RSTP can take from just a couple seconds up to around 10 seconds. 

This is because RSTP can quickly replace root ports and designated ports and lower wait times. 

RSTP switches don’t wait to receive “Hello BDPUs” before making and sending their own out. 

It also doesn’t wait on timers before learning from peers. 

RSTP also introduces the roles of the Alternate (root) port. 

The Alternate Port receives data, but is not the current root port. 

This port is a backup that takes over the role of the root port should it ever fail.

For example, if a link between a node and the root fails, the node will disable the corresponding port and put the alternate root in forwarding mode.

Because RSTP doesn’t wait on timers, the process of an alternate port taking over for root can happen in a matter of seconds. 

### RSTP Port States

Disabled / Disconnected device ports have a “discarding state” in RSTP

Blocking also becomes discarding in RSTP

There is no listening state.

There are learning and forwarding states, like STP.

RSTP avoids needing timers by having switches share the observed topology changes and provide eachother with instructions on how to adapt to those changes. 

### Backup (Designated) Ports

Backup ports are used as backups for designated ports in systems where a hub has multiple connections for a switch. This is not a common occurrence, as hubs are not as common as they used to be.

### Port Types

Point-to-point ports connect two switches that are not at the edge of a network. 

Point-to-point edge ports connect a switch to a device at the end of a network such as a server or PC

Ports connected to an Ethernet hub are “shared ports”

### Optional STP Features

Etherchannel doubles connections between nodes so if on fails, theres another line link preventing convergence. 

Despite being doubled, an Etherchannel is refferred to as a single link. 

PortFast quickly established designated ports in forwarding states without following the standard STP process.

This is used with endpoints because an STP switch port will always win the Designated Port election against endpoints that don’t use STP.

Avoid setting up PortFast with bridges and switches because it can cause forwarding loops

### BDPU Guard

Can be enabled so that if a BDPU is received on a port, that port is disabled. 
This guards against unexpected or malicious connections to other switches. 

### BDPU Filter

Can be used to disable PortFast on a switch that receives a BDPU or disable STP on a switch by discarding all BDPUs.

#### BDPU Filter to Prevent Loops on PortFast Ports

Normally, portfast ports dont get BDPU’s because it can cause a forwarding loop. 

If a switch gets plugged into other switches, they’ll start sending BDPUs.

BDPU Filter, if enabled, will see the anomoly and react by disabling PortFast, reverting the port to default STP rules and therefore avoiding loops.

#### BDPU Filter to disable STP on a Port

Say you want to connect two separate LANs, but preserve the port and switch roles. 

If the connected switches between the 2 LANs are BDPU Filtering, neither LAN as a whole will receive BDPUs from each other.

As a result, the 2 LANs are linked but keep their topologies and two separate roots. 

 

### Root Guard

Root guard is used in situations where it’s possible for switches with the worst priority to be misconfigured to take over the root position. 

To avoid this root misassignement, Root Guard shuts down ports that receive BDPUs with higher superiority, until the port stops receiving those BDPUs

If you want to use Root Guard, you should have a significant understanding of your topology and have ideas of which switches should never become root. 

### Loop Guard

Loop guard is a protocol that activates when BDPUs and a switch would otherwise become a designated port in a situation where that would not be desired.