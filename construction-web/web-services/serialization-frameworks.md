# Serialization Frameworks

Serialization is the process of converting the state of an object into a form that can be persisted or transported. The complement of serialization is deserialization, which converts a stream into an object. Together, these processes allow data to be easily stored and transferred.

### What are the applications of Data Serialization?

Serialization allows a program to save the state of an object and recreate it when needed. Its common uses are:

* **Persisting data onto files** – happens mostly in language-neutral formats such as CSV or XML. However, most languages allow objects to be serialized directly into binary using APIs such as the `Serializable` interface in Java, `fstream`class in C++, or Pickle module in Python.
* **Storing data into Databases** – when program objects are converted into byte streams and then stored into DBs, such as in Java JDBC.
* **Transferring data through the network** – such as web applications and mobile apps passing on objects from client to server and vice versa.
* **Remote Method Invocation \(RMI\)** – by passing serialized objects as parameters to functions running on a remote machine as if invoked on a local machine. This data can be transmitted across domains through firewalls.
* **Sharing data in a Distributed Object Model** – when programs written in different languages \(running on diverse platforms\) need to share object data over a distributed network using frameworks such as COM and CORBA. However, SOAP, REST and other web services have replaced these applications now.

### Data Serialization formats

#### Text-based formats:

* **XML \(Extensible Markup Language\)** - Nested textual format. Human-readable and editable. Schema based validation. Used in metadata applications, web services data transfer, web publishing.
* **CSV \(Comma-Separated Values\)** - Table structure with delimiters. Human-readable textual data. Opens as spreadsheet or plaintext. Used as plaintext Database.
* **JSON \(JavaScript Object Notation\)** - Short syntax textual format with limited data types. Human-readable. Derived from JavaScript data formats. No need of a separate parser \(like XML\) since they map to JavaScript objects. Can be fetched with an `XMLHttpRequest` call. No direct support for `DATE` data type. All data is dynamically processed. Popular format for web API parameter passing. Mobile apps use this extensively for user interaction and database services.
* **YAML \(YAML Ain't Markup Language\)** - Lightweight text format. Human-readable. Supports comments and thus easily editable. Superset of JSON. Supports complex data types. Maps easily to native data structures. Used in configuration settings, document headers, Apps with need for MySQL style self-references in relational data.

#### Binary formats:

* **BSON \(Binary JSON\)** - Created and internally used by MongoDB. Binary format, not human-readable. Deals with attribute-value pairs like JSON. Includes datetime, bytearray and other data types not present in JSON. Used in web apps with rich media data types such as live video. Primary use is storage, not network communication.
* **MessagePack** - Designed for data to be transparently converted from/to JSON. Compressed binary format, not human-readable. Supports static typing. Supports RPC. Better JSON compatibility than BSON. Primary use is network communication, not storage. Used in apps with distributed file systems.
* **protobuf \(Protocol Buffers\)** - Created by Google. Binary message format that allows programmers to specify a schema for the data. Also includes a set of rules and tools to define and exchange these messages. Transparent data compression. Used in multi-platform applications due to easy interoperability between languages. Universal RPC framework. Used in performance-critical distributed applications.

### Comparing serialization formats?

Here's a brief comparison:

* Speed – Binary formats are faster than textual formats. A late entrant, **protobuf reports the best times**. With compressed data, speed difference is even greater. For apps that aren't data intensive or real time, JSON is preferable due to readability and being schema-less. 
* Data size – This refers to the physical space in bytes post serialization. For small data, compressed JSON data occupies more space compared to binary formats like protobuf. With larger files, the gap narrows. Generally, **binary formats always occupy less space**. 
* Usability – Human readable formats like JSON are naturally preferred over binary formats. For editing data, YAML is good. For complex data types, cross-platform serialization libraries allow data structure to be defined in schemas \(for text formats\) or IDL \(for binary formats\). Schema definition is easy in protobuf, with in-built tools.
* Compatibility, extensibility – JSON is a closed format. XML is average with schema versioning. Backward compatibility \(extending schemas\) is best handled by protobuf.

### Serialization Frameworks

#### [Protobuf-net](https://github.com/protobuf-net/protobuf-net)

#### [ZeroFormatter](https://github.com/neuecc/ZeroFormatter)

#### [Json.net](https://www.newtonsoft.com/json)

#### [MessagePack](https://github.com/msgpack/msgpack-cli)

