---
tags:
  - ExamGoals
---
POE stands for Power over Ethernet.
It enables for delivering power over copper Ethernet cables, providing an alternative from using regular power cords. The addition of providing power with data in a single cable saved much time and reduced costs .

It was initially developed to scale usability for Cisco IP phones. The system took advantage of previously unused pairs in the 10/100 Mbps Ethernet cabling for these phones. This was eventually scaled up to use all four pairs of the UTP to increase max power transmission to 90W. 

The increase to 90W enabled the ability to power many different appliances. 

**Benefits of PoE**
- Cheaper to install
- Multipurpose
- Can power many different devices
- Designed to avoid power overloads via autonegotiation
- Scalable to building out networks. 

**PoE Standards**

| PoE Standard | IEEE Standard | Wattage from PSE | W from PD | Wire Pairs |
| ------------ | ------------- | ---------------- | --------- | ---------- |
| PoE          | 802.3af       | 15               | 12.95     | 2          |
| PoE+         | 802.3at       | 30               | 25.5      | 2          |
| UPoE         | 802.3bt       | 60               | 51        | 4          |
| UPoe+        | 802.3bt       | 90               | 71.3      | 4          |
*PD - Powered device
PSE - Power sourcing equipment
UPoE - Universal Power over Ethernet*

**Implementation**
A PoE switch can power a device directly

A non-PoE switch would require a PoE Injector in between the Switch and the PD.

**Autonegotiation**
As a means to not destroy equipment, PoE equipment is designed to check equipment for their supported wattage, and settle on the most efficient wattage before delivering power. 

**Common PoE Devices**
- IP phones
- Wireless APs
- IP cameras