# Filters

**Filters** in ASP.NET Core allow code to be run before or after specific stages in the request processing pipeline.

Built-in filters handle tasks such as:

* Authorization \(preventing access to resources a user isn't authorized for\).
* Response caching \(short-circuiting the request pipeline to return a cached response\).

**Custom filters** can be created to handle cross-cutting concerns. Examples of cross-cutting concerns include error handling, caching, configuration, authorization, and logging.

Filters run within the _ASP.NET Core action invocation pipeline_, sometimes referred to as the _filter pipeline_. The filter pipeline runs after ASP.NET Core selects the action to execute.

![](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters/_static/filter-pipeline-1.png?view=aspnetcore-2.1)

### Filter types

Each filter type is executed at a different stage in the filter pipeline:

* [Authorization filters](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#authorization-filters) run first and are used to determine whether the user is authorized for the request. Authorization filters short-circuit the pipeline if the request is unauthorized.
* [Resource filters](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#resource-filters):
  * Run after authorization.
  * [OnResourceExecuting](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.filters.iresourcefilter.onresourceexecuting) can run code before the rest of the filter pipeline. For example, `OnResourceExecuting` can run code before model binding.
  * [OnResourceExecuted](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.filters.iresourcefilter.onresourceexecuted) can run code after the rest of the pipeline has completed.
* [Action filters](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#action-filters) can run code immediately before and after an individual action method is called. They can be used to manipulate the arguments passed into an action and the result returned from the action.
* [Exception filters](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#exception-filters) are used to apply global policies to unhandled exceptions that occur before anything has been written to the response body.
* [Result filters](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#result-filters) can run code immediately before and after the execution of individual action results. They run only when the action method has executed successfully.

### Implementation

```csharp
public class MySampleActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
        // Do something before the action executes.
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
        // Do something after the action executes.
    }
}
```

### Built-in filter attributes

ASP.NET Core includes built-in attribute-based filters that can be subclassed and customized. For example, the following result filter adds a header to the response:

```csharp
public class AddHeaderAttribute : ResultFilterAttribute
{
    private readonly string _name;
    private readonly string _value;

    public AddHeaderAttribute(string name, string value)
    {
        _name = name;
        _value = value;
    }

    public override void OnResultExecuting(ResultExecutingContext context)
    {
        context.HttpContext.Response.Headers.Add( _name, new string[] { _value });
        base.OnResultExecuting(context);
    }
}
```

Attributes allow filters to accept arguments, as shown in the preceding example. Apply the `AddHeaderAttribute` to a controller or action method and specify the name and value of the HTTP header:

```csharp
[AddHeader("Author", "Joe Smith")]
public class SampleController : Controller
{
    public IActionResult Index()
    {
        // ...
    }
}
```

