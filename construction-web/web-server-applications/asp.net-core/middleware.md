# Middleware

{% hint style="success" %}
**Middleware** is software that's assembled into an app pipeline to handle requests and responses.
{% endhint %}

Each component:

* Chooses whether to pass the request to the next component in the pipeline.
* Can perform work before and after the next component in the pipeline.

![](../../../.gitbook/assets/image%20%2879%29.png)

The request handling pipeline is composed as a series of middleware components. Each component performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.

Example of a middleware class:

```csharp
public class SomeMiddleware
{
    private readonly RequestDelegate _next;

    public RequestSetOptionsMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext)
    {
        // some logic here, like logging, changing headers etc
        Console.WriteLine("Hello world from middleware");
        
        await _next(httpContext);
    }
}
```

Add middleware to pipeline:

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // ...
    }

    public void Configure(IApplicationBuilder app)
    {
        app.UseHttpsRedirection();
        
        // custom middleware
        app.UseMiddleware<SomeMiddleware>();
        
        app.UseStaticFiles();
        app.UseMvc();
    }
}
```

When a delegate doesn't pass a request to the next delegate, it's called **short-circuiting the request pipeline**. Short-circuiting is often desirable because it avoids unnecessary work. For example, _Static File Middleware_ can act as a **terminal middleware** by processing a request for a static file and short-circuiting the rest of the pipeline.

{% hint style="warning" %}
Do **NOT** call `next.Invoke` after the response has been sent to the client. Changes to `HttpResponse` after the response has started throw an exception \(like setting headers and a status code\). 
{% endhint %}

