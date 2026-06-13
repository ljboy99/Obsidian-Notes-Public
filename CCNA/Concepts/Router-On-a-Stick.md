Involves creating sub-interfaces based off a single existing connection, and uses dot1q encapsulation to tag and manage VLAN traffic. 

This enables inter-VLAN communication by using VLAN tagging to show where data comes from and uses the IP to saw where the data should go. The IP is used to retag the header with the new VLAN. 

RoaS uses sub interfaces
```
encapsulation dot1q 13
```
This will create encapsulation standard for the sub interface 13

