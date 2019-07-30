# Basics of Firewalls and DMZ

### Firewall

Security devices such as firewalls are the main defense for a company’s networks, whether they are LANs, WANs, intranets, or extranets. Perimeter security zones such as demilitarized zones \(DMZs\) help keep certain information open to specific users or to the public while keeping the rest of an organization’s data secret.

{% hint style="success" %}
Firewalls are primarily used to protect one network from another. They are often the first line of defense in network security. There are several types of firewalls; some run as software on server computers, some run as stand-alone dedicated appliances, and some work as just one function of many on a single device. They are commonly implemented between the LAN and the Internet.
{% endhint %}

![](../../.gitbook/assets/image%20%2845%29.png)

Many of today’s firewalls have two types of firewall technologies built into them: SPI and NAT. However, there are a couple other types of firewall methodologies of which you should be aware:

* **Packet filtering** inspects each packet that passes through the firewall and accepts or rejects it based on a set of rules. There are two types of filtering: stateless packet inspection and stateful packet inspection \(SPI\). A stateless packet filter, also known as pure packet filtering, does not retain memory of packets that have passed through the firewall. Because of this, a stateless packet filter can be vulnerable to IP spoofing attacks. However, a firewall running stateful packet inspection is normally not vulnerable to this because it keeps track of the state of network connections by examining the header in each packet. It should be able to distinguish between legitimate and illegitimate packets. This function operates at the network layer of the OSI model.
* **NAT filtering**, also known as NAT endpoint filtering, filters traffic according to ports \(TCP or UDP\). This can be done in three ways: using basic endpoint connections, by matching incoming traffic to the corresponding outbound IP address connection, or by matching incoming traffic to the corresponding IP address and port.
* **Application-level** gateway \(ALG\) supports address and port translation and checks whether the type of application traffic is allowed. For example, your company might allow FTP traffic through the firewall, but it may decide to disable Telnet traffic. The ALG checks each type of packet coming in and discards those that are Telnet packets. This adds a layer of security; however, it is resource intensive.
* **Circuit-level** gateway works at the session layer of the OSI model when a TCP or UDP connection is established. Once the connection has been made, packets can flow between the hosts without further checking. Circuit-level gateways hide information about the private network, but they do not filter individual packets.

### DMZ

A perimeter network or demilitarized zone \(DMZ\) is a small network that is set up separately from a company’s private local area network and the Internet. It is called a perimeter network because it is usually on the edge of a LAN, but DMZ has become a much more popular term.

A DMZ allows users outside a company LAN to access specific services located on the DMZ. However, when the DMZ set up properly, those users are blocked from gaining access to the company LAN. Users on the LAN quite often connect to the DMZ as well, but without having to worry about outside attackers gaining access to their private LAN. The DMZ might house a switch with servers connected to it that offer web, email, and other services.

Two common DMZ configurations are as follows:

* **Back-to-back configuration**: This configuration has a DMZ situated between two firewall devices, which could be black box appliances or Microsoft Internet Security and Acceleration \(ISA\) Servers.
* **3-leg perimeter configuration**: In this scenario, the DMZ is usually attached to a separate connection of the company firewall. Therefore, the firewall has three connections—one to the company LAN, one to the DMZ, and one to the Internet.

![](../../.gitbook/assets/image%20%2873%29.png)

In computer networks, a DMZ \(demilitarized zone\), also sometimes known as a perimeter network or a screened subnetwork, is a physical or logical subnet that separates an internal local area network \(LAN\) from other untrusted networks, usually the internet. External-facing servers, resources and services are located in the DMZ. So, they are accessible from the internet, but the rest of the internal LAN remains unreachable. This provides an additional layer of security to the LAN as it restricts the ability of hackers to directly access internal servers and data via the internet.

Any service provided to users on the public internet should be placed in the DMZ network. Some of the most common of these services include web servers and proxy servers, as well as servers for email, domain name system \(DNS\), File Transfer Protocol \(FTP\) and voice over IP \(VoIP\).

The systems running these services in the DMZ are reachable by hackers and cybercriminals around the world and need to be hardened to withstand constant attack. The term DMZ comes from the geographic buffer zone that was set up between North Korea and South Korea at the end of the Korean War.

DMZs are intended to function as a sort of buffer zone between the public internet and the organizational network. Deploying the DMZ between two firewalls means that all inbound network packets are screened using a firewall or other security appliance before they arrive at the servers the organization hosts in the DMZ. This should be enough to block the most casual of threat actors.

