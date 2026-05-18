---
tags:
  - ExamGoals
---
https://artofnetworkengineering.com/2023/08/14/ccna-series-ngfw-and-ips/
https://www.cisco.com/site/us/en/learn/topics/security/what-is-a-next-generation-firewall.html
https://www.geeksforgeeks.org/ethical-hacking/intrusion-prevention-system-ips/
https://www.certificationkits.com/cisco-certification/ccna-articles/cisco-ccna-wireless/cisco-ccna-wireless-intrustion-prevention-systemips/
https://www.networkacademy.io/ccna/network-fundamentals/intrusion-prevention-system-ips?utm_source=chatgpt.com

**Next Generation Firewalls (NGFW)**

Typically, firewalls have rules set up to be enforced across layers 3 and 4.
NGFW can enforce rules across all 7 layers. 
According to CISCO, an NGFW has:
- Standard firewall features
- Integrated IPS
- Detection for risky applications
- Threat intelligence sources
- Upgradability and adaptability

Benefits to look for in an NGFW include:
- Breach Prevention: The ability to stop attacks before they happen with high quality IPS, URL filtering and reputable providers for threat intelligence. 
- Network Visibility: Being able to see what threats are present on what networks and devices as well as when and where the threat originated. 
- Application Awareness: An NGFW should be aware of the applications sending and receiving data over a network and onto a host. 
- Flexibility: Being able to deploy across whatever system you need as well controlling what features you deploy on those systems. 
- Ability to quickly detect and prioritize threats
- Integrates with your tools 
- Automatic diagnostics and information logging. 

**Intrusion Prevention System (IPS)**
An IPS is a system which actively looks through network and system traffic to prevent attacks in real time. 
It looks at behavioral patterns of the network and automates responses against attacks. 
The two basic installations of IPS are Host based and Network based. 

- Host based IPS (HIPS)
	- protect a host on an OS level. Looks at parameters such as logs, error messages, etc.
- Network based IPS (NIPS)
	- Monitors traffic flowing across the network
	- Typically deployed inline so it can actively block malicious traffic

And then there's WIPS, which actively searches for unauthorized access through the wireless network. This can be deployed over an existing WLAN. WIPS can prevent against many attacks such as: MAC Spoofing, MITM attacks, unauthorized access, misconfigurations and more. 

How does an IPS find threats?
- Signature-based Detection: The IPS will compare every packet of data with an list of known malicious signatures and act accordingly if the a packet matches up with one of these. 
- Anomaly-based Detection: The IPS will build a recognition of common traffic patterns on the network and lookout for patterns that it does not recognize as normal. 
- Policy-Based Detection: This method uses rules set up by an administrator to create security policies and act if these policies are broken. 

Once threats are found through any of these methods, IPS may do any of the following:
- Alert and log the activity
- Discard the malicious packet
- Send a reset packet to both sides of the connection and end the communciation.
- Quarantine the affected host