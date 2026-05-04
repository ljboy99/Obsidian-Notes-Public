Cisco routers and [[Switch|switches]] use a command-line interface (CLI)

There are 3 main kinds of Cisco LAN switches:
1. Cisco Catalyst - for enterprise use
2. Cisco Nexus - for data centers
3. Cisco Meraki - for enterprises with LAN usage

The CCNA mostly refers to CISCO Catalyst switches.
A [[switch]]'s physical connectors are referred to as ports or interfaces.

Ports are identified by "Interface IOs" designated by Cisco.
	Ex. "Gigabit Ethernet 1/0/2"

Cisco has their own operating systems for their Catalyst switches called IOS and IOS XE. They are CLI based, with IOS XE having more modern and efficient features.

IOS is short for Interwork Operating System
The operating system controls switch performance and gives users a CLI interface for human input. 
You can operate a switch's CLI through it's console.

The console bridges your PC to operate a switch directly via console software.

Older switches used rollover pinout cables. In some situations you will need to use an adapter to connect your PC and control these switches. 

## Configuring a Terminal Editor
Terminals send text data inputted by a user to a switch by passing that data through the console. 
To work, an emulator must match PC port setting to the switch console port settings. 

## Accessing the CLI with Telnet and SSH
Telnet and SSH allow users to connect to another devices CLI via IP
Telnet established a client/server relationship between devices. Data processed through telnet was sent in clear text, which is a security risk. 
SSH encrypts all of the data that is communicated through the console. This stops people from being able to steal the data that is being passed along. 

## User and Enable (Privileged) Modes
Exec/user mode let's users look and perform minor functions in a system with low risk of causing damage to the system. 
Enable/Privileged mode allows for users to give systems more powerful commands.
The 'reload' command reboots Cisco IOS. This is only usable in enable mode. 

## Password Security for CLI Access from Console
You can set a password with the 'password' command. 
```
--- Example ---
enable password sandwich
```
This string would change the consoles privileged mode password to 'sandwich'. 
The password command is low-security, as it is stored as cleartext. The password can be furter encrypted. 

For a stronger password that is encrypted by default, you can use secrets. 
```
enable secret footlong
```
This would change the secret to footlong. If there is also a password set, the secret takes priority, and the password is ignored. 

## Accessing the CLI with WebUI
Cisco also provides GUI to manage switches and routers. This is now referred to as WebUI. If WebUI is set up in a network, engineers will be able to log into a WebUI portal to remotely manage equipment. 
WebUI is also equipped with some configuration options that reduce the need for CLI knowledge
Updated versions of WebUI also have CLI access without having to use SSH or Telnet. 
WebUI is very useful for remoting into devices to adjust configurations. 

## CLI Help Features
"?" can help tell you what your option are
? - provides all available commands. 
command ? - will list the paramater options for the typed command. 
com? - will list all the commands that start with whatever is before the ?. 
command param? - lists options for parameters that start with the letters before ?
command param(tab) - pressing tab will autocomplete what you're typing if there's only one possible option.
The CLI responds immediately to ? and will leave you where you were currently typing. 


## Debug and Show Commands
The ‘show’ command can provide you with the status of just about any of the switch’s features. This is presented as a ‘snapshot’ taken at the time the request was made.

‘debug’ will give you a live feed of the statuses and occurrences as they happen

## Configuring Cisco IOS Software
Configuration commands are entered when a switch is in configuration mode 

These tell switches what to do and how

Changes made by a config command go into effect as soon as you bit enter on that command  

Several config commands are possible, so you can move between subcommand modes while in configuration mode. This way, you can address different parts of the system. 

‘Context-setting commands’ will move you from one subcommand mode to another 

you can tell what configuration mode you are in by looking at the parenthesis next to the name of your machine (ex. Fred(config)# )


## Storing Switch Configuration Files

There are four main types of memory found in Cisco switches 

1. RAM - Active storage saved and used while the system is in operation 
2. Flash Memory - Stores IOS images and provides IOS at boot. Also capable of storing other types of files
3. ROM - Stores bootstrap program in charge of finding and launching the IOS into RAM. After it does this, IOS takes over all operations 
4. NVRAM - non-volatile RAM stores startup configs used when system is booted  

Cisco IOS stores config commands in a configuration file 

The two main types of config files are startup-config and running-config

startup-config handles initial configurations for when the system boots or reboots

running-config tracks configurations that run and may be changed during operations 

## Copying and Erasing Configuration Files

Because the running-config file runs off the RAM, it is essentially deleted ones the system power cycles. 

To keep any changes configurations, they need to be copied over to the startup-config file

the command for this is

```jsx
copy running-config startup-config
```

This will overwrite the current startup file with the current running configuration 

To erase all changes made to the startup file you can use any of the following lines 

```
write erase
erase startup-config
erase nvram
```