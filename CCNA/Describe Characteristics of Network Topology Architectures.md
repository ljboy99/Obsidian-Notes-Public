---
tags:
  - ExamGoals
---
https://learningnetwork.cisco.com/s/question/0D56e0000EBtd2dCQB/a-guide-to-simple-twotier-threetier-and-spineleaf-designs

https://ipcisco.com/lesson/network-topology-architectures/

**Two-Tier**
Tier 1 is the *Access Layer* where user end devices connect. 
Tier 2 is the *Distribution Layer* which takes traffic from the access layer and sends it out to the internet. 

The system is cheap and easy to maintain. Common for small offices or stores. 

**Three-Tier**
Tier 1 is the Access Layer
Tier 2 is the Distribution layer. Here, it directs traffic between departments.
Tier 3 is the Core Layer which is the networks backbone. 

A three-tier network is scalable, has fail-safes, and runs fairly quickly. 

It's good for operations with several departments and have room to grow. 

**Spine-leaf**
Leaf Layers connect to servers, storage, and other devices
Spine Layers connect the leaf switches together. 

Spine-leaf leverages Equal-Cost Multipathing to maintain high speed. 

It can always be scaled by adding leafs.

It's a fairly complex system, used for data centers.

**WAN**
A WAN is a Wide-Area-Network. It's a group of LANs that talk to each other. It uses WAN routers to move packets between WAN locations. 

Software-define WAN / SDWAN creates WANs and manage traffic on an application level. 

*Types of WAN Technologies*
Packet Switching breaks up data into packets, transfers them as quickly as possible, and rebuilds them at the end destination.

[[Router|Routers]] are a WAN technology.

Overlay networks create virtual networks over an existing network. VLANS are a basic form of overlay networks. 

Multiprotocol Label Swithcing (MPLS) uses labels to move data to save time instead of using network addresses. 

Frame Relays put data into frames and move it through a Frame Relay network. 

**SOHO**

SOHO has a router connected to the internet. A switch connects to this router and delivers network bandwidth to end user devices like Laptops and Access Points. 

Some SOHO architectures utilize an Access Point that functions as an AP, Switch and Router all in one unit. 

**On-premises and cloud**

Also known as a Private Cloud Service, this is a cloud service used to give employees access to virtual machines for their projects.

Cloud Teams in the cloud infrastructure create and give users access to virtual devices to use for their works. 

Public Cloud services give customers access to services without having their own private data center. 