# File transfer services: FTP, TFTP

FTP stands for File Transfer Protocol. It is used to send/receive file from the remote computer. FTP establishes two connections between client system and server system, one for control information and the other for data to be transfered. Control information carry commands/response. Authentication need to be done initially by way of validating username and password. Once it is done files can be transferred between two systems. FTP handles both binary and text format files.

When a FTP client requests to connect to the FTP server, a TCP connection is being established to the FTP server's port 21 reserved for FTP. After authentication is done, another TCP connection is being established for the actual data transfer on port number 20.

get,put are popular FTP commands. In order to avoid use of commands there are GUI based FTP applications have been developed, one of the popular application I have come across is FTP commander PRO another and another application is FileZilla.

TFTP stands for Trivial File Transfer Protocol.  It is simpler than FTP, does file transfer between client and server process but does not provide user authentication and other useful features supported by FTP. TFTP uses UDP while FTP uses TCP.

As TFTP is unreliable protocol due to UDP, it uses application layer recovery supported by UDP. This is done by embedding a small header between the UDP header and the data. This header incorporates codes for example read,write and acknowledgement along with numbering scheme which numbers 512 bytes of data. These block numbers provided are used to acknowledge the receipt and re-send the data in case of checksum failures. TFTP sends one block and waits on acknowledgement before sending another block.

| FTP\(File Transfer Protocol\) | TFTP\(Trivial File Transfer Protocol\) |
| :--- | :--- |
| it uses TCP port numbers 21 | it uses UDP port number 69 |
| it uses TCP as transport layer protocol | it uses UDP as transport layer protocol |
| FTP uses robust control commands | TFTP uses simple control commands |
| it sends data over a separate TCP connection from control commands | it uses no connections because UDP is connectionless protocol |
| it requires more memory and programming effort | it requires less memory and programming effort |

