# Routing

Most apps should choose a basic and descriptive routing scheme so that URLs are readable and meaningful. The default conventional route `{controller=Home}/{action=Index}/{id?}`.

Consider the following default route template:

```csharp
app.UseMvc(routes =>
{
    routes.MapRoute("default", "{controller=Home}/{action=Index}/{id?}");
});
```

Suppose you generate a link to an action using the following route:

```csharp
var link = Url.Action("ReadPost", "blog", new { id = 17, });
```

With `IRouter`-based routing, this code generates a URI of `/blog/ReadPost/17`, which respects the casing of the provided route value. Endpoint routing in ASP.NET Core 2.2 or later produces `/Blog/ReadPost/17` \("Blog" is capitalized\).

### Middleware example

In the following example, a middleware uses the `LinkGenerator` API to create link to an action method that lists store products.

```csharp
using Microsoft.AspNetCore.Routing;

public class ProductsLinkMiddleware
{
    private readonly LinkGenerator _linkGenerator;

    public ProductsLinkMiddleware(RequestDelegate next, LinkGenerator linkGenerator)
    {
        _linkGenerator = linkGenerator;
    }

    public async Task InvokeAsync(HttpContext httpContext)
    {
        var url = _linkGenerator.GetPathByAction("ListProducts", "Store");
        httpContext.Response.ContentType = "text/plain";
        await httpContext.Response.WriteAsync($"Go to {url} to see our products.");
    }
}
```

### Complex routing

The following example adds route constraints and data tokens:

```csharp
routes.MapRoute(
    name: "us_english_products",
    template: "en-US/Products/{id}",
    defaults: new { controller = "Products", action = "Details" },
    constraints: new { id = new IntRouteConstraint() },
    dataTokens: new { locale = "en-US" });
```

