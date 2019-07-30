# Application layer protocols basics \(HTTP, FTP, Telnet\)

### HTTP

The Hypertext Transfer Protocol \(HTTP\) is an application protocol for distributed, collaborative, hypermedia information systems. HTTP is the foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources that the user can easily access, for example by a mouse click in a web browser. HTTP was developed to facilitate hypertext and the World Wide Web.

HTTP functions as a request–response protocol in the client–server computing model. A web browser, for example, may be the client and an application running on a computer hosting a website may be the server. The client submits an HTTP request message to the server. The server, which provides resources such as HTML files and other content, or performs other functions on behalf of the client, returns a response message to the client. The response contains completion status information about the request and may also contain requested content in its message body.

A web browser is an example of a user agent \(UA\). Other types of user agent include the indexing software used by search providers \(web crawlers\), voice browsers, mobile apps, and other software that accesses, consumes, or displays web content.

HTTP is designed to permit intermediate network elements to improve or enable communications between clients and servers. High-traffic websites often benefit from web cache servers that deliver content on behalf of upstream servers to improve response time. Web browsers cache previously accessed web resources and reuse them, when possible, to reduce network traffic. HTTP proxy servers at private network boundaries can facilitate communication for clients without a globally routable address, by relaying messages with external servers.

HTTP is an application layer protocol designed within the framework of the Internet protocol suite. Its definition presumes an underlying and reliable transport layer protocol, and Transmission Control Protocol \(TCP\) is commonly used. However, HTTP can be adapted to use unreliable protocols such as the User Datagram Protocol \(UDP\), for example in HTTPU and Simple Service Discovery Protocol \(SSDP\).

HTTP resources are identified and located on the network by Uniform Resource Locators \(URLs\), using the Uniform Resource Identifiers \(URI's\) schemes http and https. For example, including all optional components:

![](../../.gitbook/assets/image%20%2856%29.png)



### FTP

The File Transfer Protocol \(FTP\) is a standard network protocol used for the transfer of computer files between a client and server on a computer network.

FTP is built on a client-server model architecture using separate control and data connections between the client and the server. FTP users may authenticate themselves with a clear-text sign-in protocol, normally in the form of a username and password, but can connect anonymously if the server is configured to allow it. For secure transmission that protects the username and password, and encrypts the content, FTP is often secured with SSL/TLS \(FTPS\) or replaced with SSH File Transfer Protocol \(SFTP\).

### Telnet

Telnet is a protocol used on the Internet or local area network to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection. User data is interspersed in-band with Telnet control information in an 8-bit byte oriented data connection over the Transmission Control Protocol \(TCP\).

Telnet is a protocol used on the Internet or local area network to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection. User data is interspersed in-band with Telnet control information in an 8-bit byte oriented data connection over the Transmission Control Protocol \(TCP\).

 The term telnet is also used to refer to the software that implements the client part of the protocol. Telnet client applications are available for virtually all computer platforms. Telnet is also used as a verb. To telnet means to establish a connection using the Telnet protocol, either with command line client or with a programmatic interface. 

