Different cables and connector setups may require different configurations.

## IEEE Autonegotiation Concepts

By default, most Cisco switches have autonegotiation enabled, 

NICs and switch ports can support different standards and speeds. This gives systems some modularity, allowing them to grow and change. 

Devices connected to these ports will autonegotiate to agree on the best speeds and standards to use. 

This selection of best speed and standard is achieved after both sides share information about their capabilities 

## Autonegotiation Under Working Conditions

In autonegotiation, devices send Fast Link Pulses (FLPs) which contain information about that devices speed and standards, so other devices will know that the sender supports. 

With Autonegotiation enabled, both sides will send FLPs to each other. After declaring their supported speeds and duplex, they settle to utilize the highest compatibility. 

### Having Autonegotiation Disabled

CISCO recommends not to disable autonegotiation, but devices can still work together if this happens. 
If one device in a pair has autonegotiation disabled, the device with autonegotiation enabled will eventually realize that, though they are sending them, they are not receiving FLPs. They will then adapt their speed to the rate that they are receiving incoming signals. 

This  arrangement utilizes default duplex. If a device detects speeds of 10/100 mbps, it will default to half duplex. Any faster speeds will result in full duplex. This solution, while intuitive, can cause poor performance and data collisions due to “duplex mismatch”.

## Viewing Autonegotiation In Interfaces

When you use the command:

```jsx
show interfaces status
```

your switch should output a table which will include the speed and duplexes learned by autonegotiation. Anything learned by autonegotiation is prefixed by “a-”

```jsx
a-full duplex
a-1000 #this is 1000 mbps autonegotiated
```

If a devices is not working or not connected, it’s speed and duplex will simply be listed as “auto”.

## LAN Hubs

Hubs do not use autonegotiation, Instead, they use IEEE Parallel Detection rules. Most times, this will result in speeds of 10 mbps at half duplex.

## Setting Speed and Duplex Manually

If you’re using manual configurations, you configure devices at both ends to the same speed and duplex on your own. 

*Say we want to run 1000 mbps at full duplex between two switches.*

*On Switch 1’s CLI, you will enter configuration mode on the port connected to switch 2 and enter the following:*

```jsx
speed 1000
duplex full
```

*You will then repeat this on Switch 2’s CLI on the port that is connected to Switch 1.* 

*Under this configuration, you will not see an “a-” prefix for speed or duplex when you view the interface configs. This is because these settings were not autonegotiated.* 

## Auto-MDIX on Cisco Switches

Auto-MDIX is short for Automatic Medium Dependent Interface Crossover. This allows devices to detect incorrect cable pinouts and adjust how they transmit and receive signals to accommodate for the error. 

Cisco Catalyst switches use Auto-MDIX by default , so if you were to connect two switches with a straight-thru cable instead of a crossover cable, the system will still function. 

Only one side will need to switch pins, so if Auto-MDIX is enabled on one device, and disabled on the other, the system will still function. 

Please refer to the following CLI commands for enabling and disabling Auto-MDIX

```jsx
mdix auto #this will enable auto mdix
no mdix auto #this will disable auto mdix
```

## Managing Switch Interface Configurations

“deescription” subcommand lets you store a text description to your interface

“show interface status” will show part of the description in its output

“show interface” will show the full description in its output

“interface range” is a way to apply subcommands to multiple interfaces. You will follow these keywordss with the target interfaces (ex - interface range fa0/1 - 10 | this will configure interface 1-10) (bear in mind that cisco interfaces are usually zero indexed)

When you specify a range with “interface range”, the CLI will act as though you’ve typed in the same command to every interface in that range. 

## Administratively Controlling Interface State w/ shutdown

“shutdown” - disables the interface

“no shutdown”- enables the interface 

This can also be abbreviated to “shut”/”no shut”

If you use the “shutdown” command and then view the interface with “show interface status” that interface status will show as “disabled”.

“show interfaces” would refer to the status of that interface as “administratively down”

## Removing Configurations with “no”

Some IOS configurations can be undone with the ‘no’ command. 

```jsx
no speed #revert the speed config from manual to auto
no duplex # reverts duplex to auto
no description #remove description from interface
```

Reverting all configurations that have been changed is possible. This is done with the “default interface” subcommand followed by the interface that you want this change to be applied to. Here is an example: 

```jsx
SWITCH(config)# >default interface g1/0/21
```

## Analyzing Switch Interface Status and Stats

line status and protocol status are shown when you use the ‘show interfaces’ command. Line status refers to layer 1 protocols while protocol status refers to layer 2 protocols. 

Different combinations of line and protocol statuses make up interface statuses which can be interpreted. 

Errors can still occur if both line status and protocol status are up (referred to as up/up), such as duplex mismatch. 

Duplex Mismatch can be hard to identify, as it can be present in a seemingly functional system. 

Working (up/up) interfaces will keep counters of certain events and errors that can be helpful in tracking activity and troubleshooting. 

Some errors that are counted include:

Runts - frames that have less than the minimum size requirement

Giants - frames over maximum size requirement.

Input errors - a total of several other error counters

Frame - illegally formatted frames. 

Late collisions - collisions that are typically caused by duplex mismatch

CRC - frames that do not pass FCS checks. 

Sometimes physical cabling issues can cause frames to not move properly