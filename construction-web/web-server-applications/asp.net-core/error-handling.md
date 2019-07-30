# Error Handling

### Developer Exception Page <a id="developer-exception-page"></a>

The _Developer Exception Page_ displays detailed information about request exceptions. The page is made available by `Microsoft.AspNetCore.Diagnostics` package, which is in the `Microsoft.AspNetCore.App` metapackage.

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    // ...
}
```

{% hint style="warning" %}
Enable the Developer Exception Page **only when the app is running in the Development environment**.
{% endhint %}

### Exception handler page <a id="exception-handler-page"></a>

To configure a custom error handling page for the Production environment, use the Exception Handling Middleware. The middleware:

* Catches and logs exceptions.
* Re-executes the request in an alternate pipeline for the page or controller indicated.

```csharp
if (env.IsDevelopment())
{
    // ...
}
else
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}
```

### Database error page <a id="database-error-page"></a>

The _Database Error Page middleware_ captures database-related exceptions that can be resolved by using Entity Framework migrations.

```csharp
if (env.IsDevelopment())
{
    app.UseDatabaseErrorPage();
}
```

### Exception filters <a id="exception-filters"></a>

Exception filters:

* Implement `IExceptionFilter` or `IAsyncExceptionFilter`.
* Can be used to implement common error handling policies.

```csharp
public class CustomExceptionFilterAttribute : ExceptionFilterAttribute
{
    private readonly IHostingEnvironment _hostingEnvironment;

    public CustomExceptionFilterAttribute(IHostingEnvironment hostingEnvironment)
    {
        _hostingEnvironment = hostingEnvironment;
    }

    public override void OnException(ExceptionContext context)
    {
        if (_hostingEnvironment.IsDevelopment())
        {
            var result = new ViewResult {ViewName = "CustomError"};
            context.Result = result;
        }
    }
}
```

