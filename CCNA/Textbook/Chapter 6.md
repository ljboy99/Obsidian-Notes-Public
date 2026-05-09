## Securing the Switch CLI

By default, there are no passwords or security checks to enter enable mode.

You can use simple passwords to enforce a basic security measure. This refers to the use of password-only security, which won’t require someone to identify themselves by a username.

## Config Checklist for Shared Passwords for Console, Telnet, Enable, etc

1. Protect enable mode

```jsx
enable secret *password*
!replace the keyword 'password' with your own password. 
```

1. For console, 

a. enter console config mode

```jsx
line con 0

```

b. use ‘password *password*’ to set your consoles password. (the italicized password should be replaced with your own).

c. Use the *login* subcommand on your console. 

1. For Telnet,

a. Enter config mode on all 16 telnet lines

```jsx
line vty 0 15
!remember, indexes start at 0 rather than 1
```

b. set vty password

```jsx
password *password*
```

c. use login subcommand to enable console security.

d. use “transport input all” to enable Telnet as a protocol for all lines. 

**Understand that password-only security security is generally one of the lowest levels of security available on a switch or networking device.** 

## Securing User Mode Access with Local Usernames and Passwords

Local usernames and passwords can be stored directly on the switch / console configuration.

This level of security can be used with consoles, telnet, and SSH, but not to protect enable mode. 

Each individual login is set up with a line in the console

```jsx
username name secret password
```

Where the ‘name’ is the username and the ‘password’ is the password selected by the user.

You can also use the command “no password’ to clear the remaining console access passwords. This is because these will no longer be required with the Local login security measure. 

Once you build a list of login information for your device, you will enable the local login security type with the line:

```jsx
login local
```

Remember, ‘local’ always implies that the information is stored on the switch / device in use.

---

## Local Login Setup Checklist

1. Add each login in global config: 
”username name secret password” 
2. Configure console for local logins
    1. “line con 0”
    2. “login local”
    This tells the system to prompt for a username and password and check the user input against the saved list of logins.
    3. “no password” 
    Remove any shared/global passwords (global)
3. Configure Telnet for local logins
    1. “line vty 0 15”
    enter config mode for all 16 vty lines
    2. “login local” 
    3. “no password” (optional)
    4. “transport input all” 
    Enable telnet as input protocol.

---

## Securing User Mode Access With External Authentication Servers

When a logged in user leaves configuration mode, the switch will generate a log message, detailing time, what user was active and what events took place. 

Setting up logins on every server can be redundant and time consuming. CISCO’s solution for this is referred to an Authentication, Authorization, and Accounting Server, or AAA Server for short. 

The AAA Server is what the switch will consult to figure out if you’re allowed in or not

Authentication = Who are you?

Authorization = What are you allowed to do? 

Accounting = What did you did while you were here?

The AAA Server provides networks of machines and servers with a single point of reference for security. This also means that when login information has to be changed, the changes are only done in one place, rather than on every single machine. 

AAA Servers either RADIUS or TACACS+ protocols to encrypt passwords as they move along the network. 

---

## Securing Remote Access with [[Secure Shell]]

Unlike Telnet, SSH encrypts all data transfers by default.

With this, SSH can use the same local login authentication and keep usernames and passwords secure. 

Here are some different commands used to enable either SSH or Telnet on devices:

```jsx
transport input ## this identifies protocols allowed in vty ports
transport input all ## enable support for telnet and SSH
transport input telnet ## enable support for only telnet
transport input ssh ## enable support for only SSH
```

Most companies prefer to disable telnet and allow SSH with the “transport input ssh” option. 
Many older routers default to “transport input none”. Older switches may default to “transport input all” and most new devices default to “transport input ssh”.

You can prompt the terminal to provide ssh info

```jsx
show ip ssh #this will give ssh server info
show ssh #this will give client info
```

## Enabling and Securing the WebUI

Useful commands (global)

```jsx
no ip http server #Disable HTTP (port 80)
ip http secure-server #enable HTTPS (port 443, uses TLS)
ip http authentication local #uses method for locally defined usernames
username __ priority 15 password # define one or more username and password with privilege level 15
```

Cisco recommends disabling HTTP because HTTPS is a much more secure solution. 

User accounts are defined with their privilege levels

Level 0 is user mode

Level 15 is privileged mode

## Enabling IPv4 for Remote Access

To use SSH or WebUI remotely, your switch needs an IP address. 

In the way a PC has an NIC, a switch has it’s IP assigned to an SVI (Switch Virtual Interface), which functions like an NIC. This is also referred to as a VLAN interface. 

Once the VLAN/SVI is assigned an IP, it can then send and receive packets. 

With it’s IP, a switch communicates through a subnet on a VLAN.

To communicate outside that subnet/VLAN, it needs to have a default gateway set up.

## IPv4 Setup Guide

1. Put your switch in VLAN 1 config mode

```jsx
interface vlan 1
```

1. Assign an IP address and mask

```jsx
ip address xx.x.x.xx xxx.xxx.xxx.x 
#ip address is followed by the IP and Mask
```

1. Enable the VLAN 1

```jsx
no shutdown
```

1. Configure the default gateway

```jsx
ip default-gateway xx.x.x.xx
```

## Configuring a Switch to Learn its IP Address w/ DCHP

Dynamic Host Configuration Protocol lets switches dynamically learn IP addresses.

```jsx
ip address dhep
```

When you use that command, it will assign an IP address to your device and learn about the neighboring IP addresses.

## Verifying IPv4 on a Switch

You can view your IP with any of the following commands

```jsx
show running-config
show interfaces vlan X #put your vlan number for x
show dchp lease
```

If, for some reason, DCHP fails, no IP will be shown when you try to view interfaces

## Other Useful Commands

```jsx
no logging console
```

Disable the system from printing realtime syslog messages which may interrupt when you’re typing a command.

```jsx
logging console
```

Re-enable the realtime syslog messages

```jsx
logging synchronous
```

This forces the system to present syslogs at more convenient times, like AFTER a command output it presented.

```jsx
exec-timeout M S #replace M with minutes, S with seconds
```

Sets a duration in minutes and seconds for the console to automatically log you out. This prevents unauthorized access to commands at your privilege level / under your username.