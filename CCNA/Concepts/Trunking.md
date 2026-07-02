Trunking allows for multiple VLANs to share the same physical links. This can be very useful for large systems which would otherwise require several physical connections.

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

Using the 802.1Q would send VLAN packets with 802.1Q tags attached to them. These tags will contain information telling what VLANs the data belongs to and where they need to go. 

An 802.1Q tag contains:
	TPID - Tag Potocol Identifier set to 0x8100
	PCP - Priority code point allows prioritization of traffic
	TCI - a 16 bit field that also contains the 12 bit VLAN Identifier
	DEI - Bit that says whether a frame can be dropped or not. 
	VID - Identifies VLAN that frame belongs to.

Untagged frames will be assigned to whatever is configured to be the Native VLAN. It is important that the Native VLANs match between switches. 