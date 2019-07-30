# Open Web Interface for .NET \(OWIN\)

ASP.NET Core supports the Open Web Interface for .NET \(OWIN\). OWIN allows web apps to be decoupled from web servers. It defines a standard way for middleware to be used in a pipeline to handle requests and associated responses. ASP.NET Core applications and middleware can interoperate with OWIN-based applications, servers, and middleware.

### Use OWIN

ASP.NET Core's OWIN support is deployed as part of the `Microsoft.AspNetCore.Owin` package.

OWIN middleware conforms to the OWIN specification, which requires a `Func<IDictionary<string, object>, Task>` interface, and specific keys be set \(such as `owin.ResponseBody`\).

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: https://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

To add the `OwinHello` middleware \(shown above\) to the ASP.NET Core pipeline use the `UseOwin` extension method:

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

OWIN-based servers can host ASP.NET Core apps. One such server is **Nowin**, a .NET OWIN web server:

```csharp
services.AddSingleton<IServer, NowinServer>();
```

