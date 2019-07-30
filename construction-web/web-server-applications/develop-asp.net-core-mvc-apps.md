# Develop ASP.NET Core MVC apps

ASP.NET Core is a **cross-platform, open-source framework** for building modern cloud-optimized web applications. ASP.NET Core apps are lightweight and modular, with built-in support for dependency injection, enabling greater testability and maintainability. Combined with MVC, which supports building modern web APIs in addition to view-based apps, ASP.NET Core is a powerful framework with which to build enterprise web applications.

### MVC and Razor Pages <a id="mvc-and-razor-pages"></a>

**ASP.NET Core MVC** offers many features that are useful for building web-based APIs and apps. The term MVC stands for "Model-View-Controller", a UI pattern that **breaks up the responsibilities** of responding to user requests into several parts.

**Razor Pages** is the default approach for new web applications in Visual Studio. Razor Pages offers a simpler way of building **page-based application** features, such as non-SPA forms.

If you’re building web APIs, the MVC pattern makes more sense than trying to use Razor Pages. If your project will only expose web API endpoints, you should ideally start from the Web API project template. You can evaluate whether it makes sense to adopt Razor Pages for new features or even as a wholesale migration.

### Mapping requests to responses <a id="mapping-requests-to-responses"></a>

At its heart, ASP.NET Core apps map incoming requests to outgoing responses. At a low level, this is done with middleware, and simple ASP.NET Core apps and microservices may be comprised solely of custom middleware. When using ASP.NET Core MVC, you can work at a somewhat higher level, thinking in terms of _routes_, _controllers_, and _actions_.

```csharp
app.UseMvc(routes =>;
{
    routes.MapRoute("default","{controller=Home}/{action=Index}/{id?}");
});
```

Routes can be specified on `[HttpGet]` and similar attributes, avoiding the need to add separate `[Route]` attributes. Attribute routes can also use tokens to reduce the need to repeat controller or action names, as shown below:

```csharp
[Route("[controller\]")]
public class ProductsController : Controller
{
    [Route("")] // Matches 'Products'
    [Route("Index")] // Matches 'Products/Index'
    public IActionResult Index() {}
}
```

Diagram below shows how request execution flows through filters, if configured:

![](https://docs.microsoft.com/en-us/dotnet/standard/modern-web-apps-azure-architecture/media/image7-2.png)

### Working with dependencies <a id="working-with-dependencies"></a>

ASP.NET Core has built-in support for and internally makes use of a technique known as **dependency injection**. Dependency injection is a technique that enables loose coupling between different parts of an application. Looser coupling is desirable because it makes it easier to isolate parts of the application, allowing for testing or replacement.

### Structuring the application <a id="structuring-the-application"></a>

Monolithic applications typically have a single entry point. In the case of an ASP.NET Core web application, the entry point will be the ASP.NET Core web project. However, that doesn't mean the solution should consist of just a single project. It's useful to **break up the application into different layers** in order to follow separation of concerns. Once broken up into layers, it's helpful to go beyond folders to separate projects, which can help achieve better encapsulation.

### Security <a id="security"></a>

**Authentication** is the process of comparing credentials provided with a request to those in a trusted data store, to see if the request should be treated as coming from a known entity.

**Authorization** is the process of restricting access to certain resources based on user identity.

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

### Client communication <a id="client-communication"></a>

In addition to serving pages and responding to requests for data via web APIs, ASP.NET Core apps can communicate directly with connected clients. This outbound communication can use a variety of transport technologies, the most common being WebSockets.

ASP.NET Core **SignalR** is a library that makes it simple to add real-time server-to-client communication functionality to your applications.

Real-time client communication, whether using WebSockets directly or other techniques, are useful in a variety of application scenarios. Some examples include:

* Live chat room applications
* Monitoring applications
* Job progress updates
* Notifications
* Interactive forms applications

### Deployment <a id="deployment"></a>

The first step is to publish the application, which can be done using the dotnet publish CLI command. This will compile the application and place all of the files needed to run the application into a designated folder. When you deploy from Visual Studio, this step is performed for you automatically.

![](../../.gitbook/assets/image%20%2848%29.png)

