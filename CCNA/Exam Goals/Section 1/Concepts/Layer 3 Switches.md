---
tags:
  - ExamGoals
---
https://ipcisco.com/lesson/layer-2-vs-layer-3-switch/

These are multilayer switches capable of layer 2 switching, utilizing MAC addresses, and layer 3 routing, utilizing IP addresses. 

Layer 3 can divide networks into multiple [[broadcast domains]] (like a VLAN).

Unlike usual switches, this means that each port on a single Layer 3 switch can be set up to be part of separate broadcast domains. This can reduce broadcast traffic on the overall network. 

Layer 3 switches will function in one of two ways:
**Cut Through Method** - Looks at the first packet for IP addresses and processes the following packets by MAC
**Packet-by-packet** - Looks at each packets IP address to route them. 

Having a layer 3 switch is almost like having a switch with a router built into it. 

