If you enable sticky mac addresses on a switch, Mac addresses can be retained after reloading a switch. 

```
SW1(config-if)# switchport mode access
SW1(config-if)# switchport port-security
SW1(config-if)# switchport port-security mac-address sticky
```