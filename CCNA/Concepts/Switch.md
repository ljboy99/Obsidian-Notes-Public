There are 3 main kinds of Cisco LAN switches:
1. Cisco Catalyst - for enterprise use
2. Cisco Nexus - for data centers
3. Cisco Meraki - for enterprises with LAN usage

The CCNA mostly refers to CISCO Catalyst switches.

Switches have ports that are referred to as interfaces

Cisco has their own operating systems for their Catalyst switches called IOS and IOS XE. They are CLI based, with IOS XE having more modern and efficient features.

A switch CLI can be accessed from another computer via it's console port
It can also be accessed via Telnet or SSH 

Switches have a user mode and a privileged mode. 
User mode is low security and allows for minor changes and viewing of settings.
Privileged / enable mode allows for deep changes to the system. 

[[Layer 2 Switches]]

[[Layer 3 Switches]]

The key differences between layer 2 and 3 switches includes:
- Obviously, the layers they operate on. Keep in mind, layer 3 switches use BOTH layers 2 and 3.
- Layer 2 switches only use MAC, Layer 3 uses MAC and IP.
- Layer 3 can have multiple broadcast domains, layer 2 uses one. 
- Layer 2 switches are generally faster than layer 3 Switches
- Layer 2 switches can only communicate in their network, Layer 3 switches can use their routing capabilities to communicate with the outside world.