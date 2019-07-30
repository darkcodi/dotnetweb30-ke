# gRPC on ASP.NET Core

[gRPC](https://grpc.io/docs/guides/) is a language agnostic, high-performance Remote Procedure Call \(RPC\) framework. For more on gRPC fundamentals, see the [gRPC documentation page](https://grpc.io/docs/).

![](../../.gitbook/assets/image%20%28120%29.png)

The main benefits of gRPC are:

* Modern high-performance lightweight RPC framework.
* Contract-first API development, using Protocol Buffers by default, allowing for language agnostic implementations.
* Tooling available for many languages to generate strongly-typed servers and clients.
* Supports client, server, and bi-directional streaming calls.
* Reduced network usage with Protobuf binary serialization.

These benefits make gRPC ideal for:

* Lightweight microservices where efficiency is critical.
* Polyglot systems where multiple languages are required for development.
* Point-to-point real-time services that need to handle streaming requests or responses.

While a C\# implementation is currently available on the official gRPC page, the current implementation relies on the native library written in C \(gRPC C-core\). Work is currently in progress to provide a new implementation based on the Kestrel HTTP server and the ASP.NET Core stack that is fully managed. The following documents provide an introduction to building gRPC services with this new implementation.

[Read more](https://docs.microsoft.com/en-us/aspnet/core/tutorials/grpc/grpc-start?view=aspnetcore-3.0&tabs=visual-studio)

