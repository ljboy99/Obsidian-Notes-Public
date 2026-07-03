Loopback interfaces are software-only interfaces that emulate a physical interface. It is accessible from any physical interface on the device, and therefore not tied to a single interface.

They are often used as test IPs or as a stable identifier for management because they never go down. 

Loopback interfaces can be established with the following command:
```
R1(config)# interface loopback(number)

or 

R1(config)# int l(number)
```

If the interface does not yet exist, it will be created. It can be assigned a name and IP like other interfaces. 

Say we want to delete an existing loopback 0 interface. You would use:

```
R1(config)# no interface loopback0
or 
R1(config)# no int l0
```

Remember this only works on loopbacks because they are software based. You cannot 'delete' a physical interface via the CLI.

 