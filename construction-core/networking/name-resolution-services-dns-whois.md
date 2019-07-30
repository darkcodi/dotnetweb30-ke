# Name resolution services: DNS, whois

The hostname system was developed early in the history of TCP/IP. In this system, each computer is assigned an alphanumeric name called a hostname. If the operating system encounters an alphanumeric name where it is expecting an IP address, the operating system consults a hosts file. The hosts file contains a list of hostname-to-IP-address associations. If the alphanumeric name is on the list of hostnames, the computer reads the IP address associated with the name. The computer then replaces the hostname in the command with the corresponding IP address and executes the command.

The designers of DNS wanted to avoid having to keep an up-to-date name resolution file on each computer. DNS instead places name resolution data on one or more special servers. The DNS servers provide name resolution services for the network. If a computer on the network encounters a hostname where it is expecting an IP address, it sends a query to the server asking for the IP address associated with the hostname. If the DNS server has the address, it sends the address back to the requesting computer. The computer then invisibly substitutes the IP address for the hostname and executes the command. When a change occurs on the network \(such as a new computer or a change to a hostname\), the network administrator only has to change the DNS configuration once \(on the DNS server\). The new information will then be available to any computer that initiates a DNS query to the server. Also, the DNS server can be optimized for search speed and can support a larger database than would be possible with each computer searching separately through the cumbersome hosts file.

{% hint style="success" %}
WHOIS \(pronounced as the phrase "who is"\) is a query and response protocol that is widely used for querying databases that store the registered users or assignees of an Internet resource, such as a domain name, an IP address block or an autonomous system, but is also used for a wider range of other information. The protocol stores and delivers database content in a human-readable format.
{% endhint %}

**whois** searches for an object in a WHOIS database. WHOIS is a query and response protocol that is widely used for querying databases that store the registered users of an Internet resource, such as a domain name or an IP address block, but is also used for a wider range of other information.

Most modern versions of whois try to guess the right server to ask for the specified object. If no guess can be made, whois will connect to whois.networksolutions.com for NIC handles or whois.arin.net for IPv4 addresses and network names.  


![](../../.gitbook/assets/image%20%2813%29.png)

