**VLAN Routing With Router 802.1Q Trunks**

ROAS gives a router an interface to connect to each VLAN. This Can give the router a Unique IP for each ULAN. 
This is done through a single physical connection by utilizing virtual subinterfaces, each having their own IP address. 

Examples of subinterface names may be G0/0/0.10 or G0/0/0.20. Remember that these live on the same virtual interface. 

**How To Configure 802.1Q Trunking on a Router**
1. In global configuration mode:
```
interface type number.subinterface
```
2. Enter subinterface configuration mode and use
```
encapsulation dot1q vlan_id
```
3. Use
```
ip address <address> <mask>
```

**Define a Native VLAN**
a. Configure IP on interface without encapsulation command
or
b. Configure ip followed by 
```
encapsulation dot1q <vlan-id> native
```

