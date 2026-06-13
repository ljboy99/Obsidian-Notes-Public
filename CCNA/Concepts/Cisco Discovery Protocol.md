https://learningnetwork.cisco.com/s/article/cisco-discovery-protocol-cdp-x
https://www.geeksforgeeks.org/computer-networks/what-is-cisco-discovery-protocol-cdp/

CPD is a level 2 protocol which allows adjacent devices to discover each other and share information, configs, and device details. 

Bear in mind, CDP only functions with devices that are directly connected to eachother by wire. 

This protocol shares information by sending out CDP packets, and also allows devices to be aware that their neighbors are still active, as, by default, packets are sent every 60 seconds, and are retained for 180 seconds.

A CDP table is maintained on devices, and is updated when new CDP packets are received. An entry is wiped after the hold timer end. 

Cisco devices have CDP enabled by default

CDP Commands:

| Command                   | Function                                                                                                                                                                                       |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cdp run                   | enables CDP on a device                                                                                                                                                                        |
| no cdp run                | disables CDP on a device                                                                                                                                                                       |
| cdp enable                | enables CDP on an interface if CDP is enabled globally                                                                                                                                         |
| no cdp enable             | disables CDP on an interface                                                                                                                                                                   |
| cdp timer (seconds)       | Sets CDP packet transmission frequencey (default 60s)                                                                                                                                          |
| cdp holdtime (seconds)    | Sets how long CDP packets are held (default 180)                                                                                                                                               |
| clear cdp counters        |                                                                                                                                                                                                |
| clear cdp table           |                                                                                                                                                                                                |
| show cdp                  |                                                                                                                                                                                                |
| show cdp interface        |                                                                                                                                                                                                |
| show cdp neigbors         | This will provide a quick summary table of the neighboring connected devices.                                                                                                                  |
| show cdp entry (hostname) | You can use this to view info for a specific connected device by the hostname. You will see the platform type and IOS version. You can also use * instead of a device name to see all devices. |

CDP commands will give info about the connected devices such as the hostnames, the port that the host is connected to it by, and the port you're connected to on that device. 

CDP works on SNAP formatted media types such as Ethernet, PPP, or HDLC.

CDP messages will contain information about IOS version, IP address, device names, hardware, etc

