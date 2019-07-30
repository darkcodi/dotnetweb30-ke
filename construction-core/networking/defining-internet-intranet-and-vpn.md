# Defining internet, intranet and VPN

### Internet

The internet is a large scale client server system which uses a TCP/IP, a set of protocols which provides end-to-end connectivity specifying how data should be packetized, addressed, transmitted, routed and received at the destination. The World Wide Web, email, chat and file transfer services are all made possible by the internet.

### Intranet

An intranet is a local or restricted communications network, especially a private network created using World Wide Web software. The Intranet is guided by Internet Protocols like HTTP and TCP/IP. In simple terms, it can be said as a private network accessible only to an organization’s staff.

The intranet changed the way how corporations operate. In an intranet, network applications can be created that can run on many types of computers. It is a secure network, as it is protected by a firewall. The firewall acts as the gate keeper between a device and the network, foreseeing security of incoming and outgoing network traffic.

### VPN

VPN\(Virtual Private Network\) - is a service that lets you access the web safely and privately by routing your connection through a server and hiding your online actions.

A virtual private network \(VPN\) is a connection between two or more computers or devices that are not on the same private network. In fact, there could be LANs or WANs in between each of the VPN devices. In order to ensure that only the proper users and data sessions cross to a VPN device, data encapsulation and encryption are used. A “tunnel” is created, so to speak, through the LANs and WANs that might intervene; this tunnel connects the two VPN devices together. Every time a new session is initiated, a new tunnel is created. Some technicians refer to this as tunneling through the Internet, although some VPN tunnels might go through private networks as well.

You start the VPN client \(software\) from your VPN service. This software encrypts your data, even before your Internet Service Provider or the coffee shop WiFi provider sees it. The data then goes to the VPN, and from the VPN server to your online destination — anything from your bank website to a video sharing website to a search engine. The online destination sees your data as coming from the VPN server and its location, and not from your computer and your location.

* **PPTP**\(Point-To-Point Tunneling Protocol\). This is one of the oldest protocols in use, originally designed by Microsoft. Pros: works on old computers, is a part of the Windows operating system, and it’s easy to set up. Cons: by today’s standards, it’s barely secure. Avoid a provider if this is the only protocol offered.
* **L2TP/IPsec**\(Layer 2 Tunneling Protocol\). This is a combination of PPTP and Cisco’s L2F protocol. The concept of this protocol is sound — it uses keys to establish a secure connection on each end of your data tunnel — but the execution isn’t very safe. The addition of the IPsec protocol improves security a bit, but there are reports of NSA’s alleged ability to break this protocol and see what’s being transmitted. No matter if those are actually true, the fact that there’s a debate at all is perhaps enough to avoid this as well.
* **OpenVPN**. This takes what’s best in the above protocols and does away with most of the flaws. It’s based on SSL/TLS and it’s an open source project, which means that it’s constantly being improved by hundreds of developers. It secures the connection by using keys that are known only by the two participating parties on either end of the transmission. Overall, it’s the most versatile and secure protocol out there.

