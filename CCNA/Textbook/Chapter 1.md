[[network|Networks]] bring different devices to work together. They also work off of everchanging rules and protocols.

Networking Model - Set of documents where each part describes a function which contributes to the network. Network models ensure structure for a network to function.

[[Protocols|Protocol]] - ruleset for devices to communicate.

Requests for Comment (RFC) - Adds specific details to the broader definitions of a layer function.

Enterprise Network - network made by a corporation to allow employees to communicate.

SOHO - Small office / Home office. Smaller home networks that are used for business.

[[TCP-IP|TCP/IP]] Networking Model came from a need for a vendor-neutral network model. It defines and uses protocols to let computers communicate.

Before TCP/IP, vendors all had their own proprietary network models and network engineers would have to figure out how to get several different systems to work together to function as a network.

## [[TCP-IP|TCP/IP Application Layer]]

Defines the services that applications need to run.

This layer essentially is the bridge between your software and the network it operates on.

The most popular TCP/IP application is the web browser.

When you navigate to a website, your browser is asking for a file from a server. If the server successfully delivers that requested file, it is then displayed on your browser.

## HTTP [[Protocols|Protocol]] Mechanism

Hypertext Transfer Protocol is used when a web pages is requested and delivered.

In this process, the browser sends a “get” request in an HTTP header.

The server would then respond with a “code 200”, equivalent to saying “OK”, if the request can be done.

After success, the serve will deliver the requested data.

## [[TCP-IP|TCP/IP Transport Layer]]

Transmission Control Protocol (TCP)

User Diagram Protocol (UDP)

These protocols provide services to the application layer

## TCP Error Recovery Basics

TCP/IP keeps mechanisms to respond to issues that may occur such as lost or undelivered data.

## Adjacent-Layer Interaction

Once an error occurs, different layers may need to communicate to figure out how to respond to the issue. For example, when a request is lost, one layer may call upon another to repeat the request after not seeing the data it expected.

## Same Layer Interaction

When computers talk on the same layer, they use headers to pass information across.

## [[TCP-IP|TCP/IP Network Layer]]

Internet Protocol (IP) is the main network layer.

Much like a postal service, IP works off of addresses and routing. The upper application and transport layers will act as the person who sends out a letter. The requested address that this “letter” is sent out to will decide how IP will route the request. After the request is sent, the lower network layers do the work of understanding the pathways needed to deliver the messages and completing that delivery.

## Internet Protocol Addressing Basics

Each TCP/IP device needs an address to be identified and grouped by.

## [[Router]]

Connects devices in the TCP/IP Network by routing IP packets to/from addresses

## IP Routing Basics

Any devices with an IP address can send IP packets through the TCP/IP Network.

## TCP/IP Data-Link and Physical Layers

Defines rules for hardware in a physical network

Data-Link layer moves packets for the network layer

Data moves through encapsulated IP packets through Ethernet. It is received as electrical signals and de-encapsulated by the router.

## [[Data Encapsulation]]

Encapsulation - a process which wraps raw data in headers and footers that will provide further layers with information on what to do and how to pass data onto the next layer.

Data provided by a higher layer is encapsulated by the next layer

## TCP/IP hosts send data in a 5 step process.

1. Create and encapsulate the application data
2. Encapsulate application data in transport layer header
3. Encapsulate data supplied by transport layer in network layer header
4. Encapsulate data from network layer into Data-Link layer header and trailer
5. Transmit the bits to recipient.