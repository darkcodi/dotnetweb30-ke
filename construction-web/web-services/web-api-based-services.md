# Web API-based services

### What is Web Services?

As described by the World Wide Web Consortium \(W3C\), Web services provide a standard means of interoperating between different software applications, running on a variety of platforms and/or frameworks. Web services are characterized by their great interoperability and extensibility, as well as their machine-processable descriptions thanks to the use of XML. They can be combined in a loosely coupled way in order to achieve complex operations. Programs providing simple services can interact with each other in order to deliver sophisticated added-value services.

Web services communicate over a network through HTTP between the two systems. Many web services are identical to SOA \(Services Oriented Architecture\) and mainly rely on standards such as XML-RPC and SOAP \(Simple Object Access Protocol\).

### Advantages of Web services

There are many advantages of using web services:

* **Interoperability**: One of the advantages of web service is interoperability. Web services allow applications to communicate, exchange data and share services among themselves.The common standards-based communications methods have been developed and these make it possible for web service to be the platform-independent.  
* **Usability**: Web services are designed to be used like a web page request and receive data. Web services are the same. The capability of web services varies from simple information lookup to complex algorithmic computations. That’s why it can be easily used.
* **Reusability**: Web Services are designed to be combined to deliver more added-value services. Web services serve as building blocks to makes it easy to reuse Web Service components in other services. Also, legacy applications can be wrapped into web services to be used by others.
* **Deployability**: Web Services are deployed over Internet standards such as standard Apache, Axis2 to provide HTTP, WSDL driven services. This makes it simple to deploy.
* **Cost**: The cost is reduced due to new systems are assembled from packaged web services. The saved cost can be a benefit to both the solution provider and the customer. Moreover, efficiency is achieved at the same time.

### Types of Web services

There are two major types of web services:

* **SOAP Web Services**: SOAP \(Simple Object Access Protocol\) is an XML-based protocol for accessing web services. Its interface is described in a machine-processable format called WSDL \(Web Service Definition Language\) document. A web service is described by using a standard, formal XML notion that provides all necessary details like message format, transport protocols, and location to interact with the web service.
* **REST Web Services**: REST \(Representational State Transfer\) is a style of software architecture. The data format is described by using JSON schema notation, and it requires the use of the HTTP transport protocol.

There are some important differences between SOAP and REST

| **SOAP** | **REST** |
| :--- | :--- |
| SOAP is a protocol. | REST is an architectural style. |
| SOAP can’t use REST because it is a protocol. | REST can use SOAP web services because it is a concept and can use any protocol like HTTP, SOAP. |
| SOAP only permits XML. | REST permits many different data formats including plain text, HTML, XML, and JSON… |
| SOAP requires more bandwidth and more resources. | REST requires less bandwidth and less resources. |
| SOAP supports both SMTP and HTTP protocols. | REST requires the use of HTTP only. |
| SOAP is more reliable than REST. | REST is less secure than SOAP. |
| In most cases, SOAP is faster than REST. | REST is slower than SOAP. |
| SOAP defines its own security. | RESTful web services inherit security measures from the underlying transport. |

### The differences between Web Services vs API

API stands for Application Programming Interface which is a protocol used as an interface by software components to communicate with each other. An API serves as an interface between two different applications so that they can communicate with each other.

APIs and Web Services both are means of communication between service providers and service consumers. They are usually mistaken for each other but there are many differences between them:

| **WEB SERVICE** | **API** |
| :--- | :--- |
| All web services are APIs. | All APIs are not web services. |
| It can only be hosted on IIS. | It can be hosted within an application or IIS. |
| It is not open source but can be used by any client that understands XML. | It is open source and it can be used by any client that understands JSON or XML. |
| It requires a SOAP protocol to receive and send data over the network, so it is not a light-weight architecture. | It is light-weight architectured and good for devices which have limited bandwidth, like mobile devices. |
| A Web service uses only three styles of use: SOAP, REST and XML-RPC for communication. | API may use any style of communication. |
| It only supports the HTTP protocol. | It supports the HTTP protocol: URL, Request/Response Headers, caching, versioning, content formats. |

