# Basic troubleshooting tools \(ICMP, ping, traceroute\)

**Internet Control Message Protocol \(ICMP\)** ICMP is a Network layer protocol that belongs to the group of control protocols similar to ARP and RARP. ICMP protocol has been designed with the unreliable characteristics of the IP protocol in mind. Due to this unreliability and connectionless behavior of IP, there was no way of informing the originator host that something went wrong during data transmission. ICMP has been designed to provide this function.

ICMP messages report back to the sender when something unexpected occurs, giving the person a clue of what might have gone wrong. I want to remind you that ICMP does not solve the reliability issues of IP; that is up to the upper layer \(the Transport layer\) to perform.

The **PING** utility is one of the most famous and most helpful networking commands. It's the first command that comes to mind when facing network reachability problems. It's also the first command that needs to be issued when there is a need to find out whether a certain host is "alive" or not. The ping command uses the services of the Internet Control Message Protocol \(ICMP\), the latter being encapsulated in the IP header. Therefore, the ping utility operates basically on layer 3 \(the Network layer\) of the OSI model. It does not use the services of the Transport layer, and the reason for that is that traffic reliability issues are not the case here. Ping performs a simple host lookup.

![](../../.gitbook/assets/image%20%2863%29.png)

**TRACEROUTE** is another very helpful utility that operates similarly to ping and also uses the services of the ICMP protocol. Traceroute, as the name implies, is used to trace the path between the sender and the destination host. It is a one-way trace, meaning that it traces the route from the source to destination and not the other way around, which by the way, may follow a different path. Traceroute also uses the services of User Datagram Protocol \(UDP\), in specific implementations, as the transport layer for a specific reason that we'll go into further on.

![](../../.gitbook/assets/image%20%2853%29.png)

