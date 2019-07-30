# Understanding networks: layers and protocols

{% hint style="info" %}
 A `network protocol` is a set of rules for communicating between computers. Protocols govern format, timing, sequencing, and error control
{% endhint %}

### _**What is OSI?**_

The Open Systems Interconnection model \(OSI model\) is a conceptual model that characterizes and standardizes the communication functions of a telecommunication or computing system without regard to its underlying internal structure and technology. Its goal is the interoperability of diverse communication systems with standard communication protocols. The model partitions a communication system into abstraction layers. The original version of the model defined seven layers.

A layer serves the layer above it and is served by the layer below it. For example, a layer that provides error-free communications across a network provides the path needed by applications above it, while it calls the next lower layer to send and receive packets that constitute the contents of that path. Two instances at the same layer are visualized as connected by a horizontal connection in that layer.

The model is a product of the Open Systems Interconnection project at the International Organization for Standardization \(ISO\).

![Layer architecture](../../.gitbook/assets/image%20%28110%29.png)

### _**Why does the OSI model matter?**_ 

Although the modern Internet doesn’t strictly follow the OSI model \(it more closely follows the simpler Internet protocol suite\), the OSI model is still very useful for troubleshooting network problems. Whether it’s one person who can’t get their laptop on the internet, or a web site being down for thousands of users, the OSI model can help to break down the problem and isolate the source of the trouble. If the problem can be narrowed down to one specific layer of the model, a lot of unnecessary work can be avoided.

### _**What are the seven layers of the OSI model?**_

The seven abstraction layers of the OSI model can be defined as follows, from top to bottom:![The Application Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/7-application-layer.svg)

**7. The Application Layer**

This is the only layer that directly interacts with data from the user. Software applications like web browsers and email clients rely on the application layer to initiate communications. But it should be made clear that client software applications are not part of the application layer; rather the application layer is responsible for the protocols and data manipulation that the software relies on to present meaningful data to the user. Application layer protocols include [HTTP](https://www.cloudflare.com/learning/ddos/glossary/hypertext-transfer-protocol-http/) as well as SMTP \(Simple Mail Transfer Protocol is one of the protocols that enables email communications\).![The Presentation Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/6-presentation-layer.svg)

_**Protocols:**_ RDP, HTTP, SMTP, SNMP, POP3, FTP, SIP, TELNET

**6. The Presentation Layer**

This layer is primarily responsible for preparing data so that it can be used by the application layer; in other words, layer 6 makes the data presentable for applications to consume. The presentation layer is responsible for translation, encryption, and compression of data.

Two communicating devices communicating may be using different encoding methods, so layer 6 is responsible for translating incoming data into a syntax that the application layer of the receiving device can understand.

If the devices are communicating over an encrypted connection, layer 6 is responsible for adding the encryption on the sender’s end as well as decoding the encryption on the receiver's end so that it can present the application layer with unencrypted, readable data.

Finally the presentation layer is also responsible for compressing data it receives from the application layer before delivering it to layer 5. This helps improve the speed and efficiency of communication by minimizing the amount of data that will be transferred.![The Session Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/5-session-layer.svg)

_**Protocols:**_ XML, JSON, XDR

**5. The Session Layer**

This is the layer responsible for opening and closing communication between the two devices. The time between when the communication is opened and closed is known as the session. The session layer ensures that the session stays open long enough to transfer all the data being exchanged, and then promptly closes the session in order to avoid wasting resources.

The session layer also synchronizes data transfer with checkpoints. For example, if a 100 megabyte file is being transferred, the session layer could set a checkpoint every 5 megabytes. In the case of a disconnect or a crash after 52 megabytes have been transferred, the session could be resumed from the last checkpoint, meaning only 50 more megabytes of data need to be transferred. Without the checkpoints, the entire transfer would have to begin again from scratch.![The Transport Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/4-transport-layer.svg)

_**Protocols:**_ PAP, SDP, SCP, RPC, L2TP

**4. The Transport Layer**

Layer 4 is responsible for end-to-end communication between the two devices. This includes taking data from the session layer and breaking it up into chunks called segments before sending it to layer 3. The transport layer on the receiving device is responsible for reassembling the segments into data the session layer can consume.

The transport layer is also responsible for flow control and error control. Flow control determines an optimal speed of transmission to ensure that a sender with a fast connection doesn’t overwhelm a receiver with a slow connection. The transport layer performs error control on the receiving end by ensuring that the data received is complete, and requesting a retransmission if it isn’t.![The Network Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/3-network-layer.svg)

_**Protocols:**_ TCP, UDP, SCTP

**3. The Network Layer**

The network layer is responsible for facilitating data transfer between two different networks. If the two devices communicating are on the same network, then the network layer is unnecessary. The network layer breaks up segments from the transport layer into smaller units, called packets, on the sender’s device, and reassembling these packets on the receiving device. The network layer also finds the best physical path for the data to reach its destination; this is known as routing.![The Data Link Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/2-data-link-layer.svg)

_**Protocols:**_ IP, OSPF, RIP, IPX

**2. The Data Link Layer**

The data link layer is very similar to the network layer, except the data link layer facilitates data transfer between two devices on the SAME network. The data link layer takes packets from the network layer and breaks them into smaller pieces called frames. Like the network layer, the data link layer is also responsible for flow control and error control in intra-network communication \(The transport layer only does flow control and error control for inter-network communications\).![The Physical Layer](https://www.cloudflare.com/img/learning/ddos/glossary/open-systems-interconnection-model-osi/1-physical-layer.svg)

_**Protocols:**_ ETHERNET, PPP, HDLC

**1. The Physical Layer**

This layer includes the physical equipment involved in the data transfer, such as the cables and switches. This is also the layer where the data gets converted into a bit stream, which is a string of 1s and 0s. The physical layer of both devices must also agree on a signal convention so that the 1s can be distinguished from the 0s on both devices.

_**Protocols:**_ Bluetooth, WI-FI, ETHERNET, GSM

