# SingalR

### What is SignalR?

ASP.NET Core SignalR is an open-source library that simplifies adding real-time web functionality to apps. Real-time web functionality enables server-side code to push content to clients instantly.

Good candidates for SignalR:

* Apps that require high frequency updates from the server. Examples are gaming, social networks, voting, auction, maps, and GPS apps.
* Dashboards and monitoring apps. Examples include company dashboards, instant sales updates, or travel alerts.
* Collaborative apps. Whiteboard apps and team meeting software are examples of collaborative apps.
* Apps that require notifications. Social networks, email, chat, games, travel alerts, and many other apps use notifications.

SignalR provides an API for creating server-to-client remote procedure calls \(RPC\). The RPCs call JavaScript functions on clients from server-side .NET Core code.

Here are some features of SignalR for ASP.NET Core:

* Handles connection management automatically.
* Sends messages to all connected clients simultaneously. For example, a chat room.
* Sends messages to specific clients or groups of clients.
* Scales to handle increasing traffic.

### Transports

SignalR supports several techniques for handling real-time communications:

* WebSockets
* Server-Sent Events
* Forever Frames
* Long Polling

SignalR automatically chooses the best transport method that is within the capabilities of the server and client.

### Hubs

SignalR uses hubs to communicate between clients and servers.

A hub is a high-level pipeline that allows a client and server to call methods on each other. SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server and vice versa. You can pass strongly-typed parameters to methods, which enables model binding. SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on MessagePack. MessagePack generally creates smaller messages compared to JSON.

Hubs call client-side code by sending messages that contain the name and parameters of the client-side method. Objects sent as method parameters are deserialized using the configured protocol. The client tries to match the name to a method in the client-side code. When the client finds a match, it calls the method and passes to it the deserialized parameter data.

![](../../.gitbook/assets/image1.png)

#### Configure SignalR hubs

The SignalR middleware requires some services, which are configured by calling services.AddSignalR.

```csharp
services.AddSignalR();
```

When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure`method.

```csharp
app.UseSignalR(route =>
{
    route.MapHub<ChatHub>("/chathub");
});
```

#### Create and use hubs

Create a hub by declaring a class that inherits from Hub, and add public methods to it. Clients can call methods that are defined as public.

```csharp
public class ChatHub : Hub
{
    public Task SendMessage(string user, string message)
    {
        return Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}
```

You can specify a return type and parameters, including complex types and arrays, as you would in any C\# method. SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.

{% hint style="info" %}
Hubs are transient:

* Don't store state in a property on the hub class. Every hub method call is executed on a new hub instance.
* Use `await` when calling asynchronous methods that depend on the hub staying alive. For example, a method such as `Clients.All.SendAsync(...)` can fail if it's called without `await` and the hub method completes before `SendAsync` finishes.
{% endhint %}

### Users and groups

#### Users in SignalR

SignalR allows you to send messages to all connections associated with a specific user. By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier. A single user can have multiple connections to a SignalR app. For example, a user could be connected on their desktop as well as their phone. Each device has a separate SignalR connection, but they're all associated with the same user. If a message is sent to the user, all of the connections associated with that user receive the message. The user identifier for a connection can be accessed by the `Context.UserIdentifier` property in your hub.  
Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

#### Groups in SignalR

A group is a collection of connections associated with a name. Messages can be sent to all connections in a group. Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application. A connection can be a member of multiple groups. This makes groups ideal for something like a chat application, where each room can be represented as a group. Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.

```csharp
public async Task AddToGroup(string groupName)
{
    await Groups.AddToGroupAsync(Context.ConnectionId, groupName);
    await Clients.Group(groupName).SendAsync("Send", $"{Context.ConnectionId} has joined the group {groupName}.");
}

public async Task RemoveFromGroup(string groupName)
{
    await Groups.RemoveFromGroupAsync(Context.ConnectionId, groupName);
    await Clients.Group(groupName).SendAsync("Send", $"{Context.ConnectionId} has left the group {groupName}.");
}
```

Group membership isn't preserved when a connection reconnects. The connection needs to rejoin the group when it's re-established. It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.

To protect access to resources while using groups, use authentication and authorization functionality in ASP.NET Core. If you only add users to a group when the credentials are valid for that group, messages sent to that group will only go to authorized users. However, groups are not a security feature. Authentication claims have features that groups do not, such as expiry and revocation. If a user's permission to access the group is revoked, you have to manually detect that and remove them from the group.

### [Publish to Azure](https://docs.microsoft.com/en-us/aspnet/core/signalr/publish-to-azure-web-app?view=aspnetcore-3.0)

### Clients

* \*\*\*\*[**SignalR .NET Client**](https://docs.microsoft.com/en-us/aspnet/core/signalr/dotnet-client?view=aspnetcore-3.0)\*\*\*\*
* \*\*\*\*[**SignalR JavaScript client**](https://docs.microsoft.com/en-us/aspnet/core/signalr/javascript-client?view=aspnetcore-3.0)\*\*\*\*
* \*\*\*\*[**SignalR Java client**](https://docs.microsoft.com/en-us/aspnet/core/signalr/java-client?view=aspnetcore-3.0)\*\*\*\*

