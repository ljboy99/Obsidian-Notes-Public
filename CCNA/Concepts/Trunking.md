Trunking allows for multiple VLANs to share the same physical links.
Traffic is dictated by VLAN tags that are carried by packets. 
Before you put a link between switches into trunking mode, it needs a standard to adhere to. 

Because of this, if you try to tell a switch with an encapsulation mode of auto to trunk, the command will fail. You will first need to manually apply a trunking standard to that switch. 

An example would be to tell the switch to use the 802.1q standard protocol
```
switchport trunk encapsulation dot1q
```

and then you can enable trunking after

```
switchport mode trunk
```

