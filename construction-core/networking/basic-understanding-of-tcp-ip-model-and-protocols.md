# Basic understanding of TCP/IP model and protocols

The Internet protocol suite is the conceptual model and set of communications protocols used in the Internet and similar computer networks. It is commonly known as TCP/IP because the foundational protocols in the suite are the Transmission Control Protocol \(TCP\) and the Internet Protocol \(IP\).

The Internet protocol suite provides end-to-end data communication specifying how data should be packetized, addressed, transmitted, routed, and received. This functionality is organized into four abstraction layers, which classify all related protocols according to the scope of networking involved. From lowest to highest, the layers are the link layer, containing communication methods for data that remains within a single network segment \(link\); the internet layer, providing internetworking between independent networks; the transport layer, handling host-to-host communication; and the application layer, providing process-to-process data exchange for applications.

The technical standards underlying the Internet protocol suite and its constituent protocols are maintained by the Internet Engineering Task Force \(IETF\). The Internet protocol suite predates the OSI model, a more comprehensive reference framework for general networking systems.

Despite using a different concept for layering than the OSI model, these layers are often compared with the OSI layering scheme in the following manner:

* The Internet application layer maps to the OSI application layer, presentation layer, and most of the session layer.
* The TCP/IP transport layer maps to the graceful close function of the OSI session layer as well as the OSI transport layer.
* The internet layer performs functions as those in a subset of the OSI network layer.
* The link layer corresponds to the OSI data link layer and may include similar functions as the physical layer, as well as some protocols of the OSI's network layer.

