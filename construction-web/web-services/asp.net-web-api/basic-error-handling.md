# Basic error handling

### Developer Exception Page

The Developer Exception Page displays detailed information about request exceptions. The page is made available by the Microsoft.AspNetCore.Diagnostics package. Add code to the Startup.Configure method to enable the page when the app is running in the Development environment:

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```

Place the call to UseDeveloperExceptionPage before any middleware that you want to catch exceptions.

{% hint style="warning" %}
Enable the Developer Exception Page only when the app is running in the Development environment. You don't want to share detailed exception information publicly when the app runs in production.
{% endhint %}

The page includes the following information about the exception and the request:

* Stack trace
* Query string parameters \(if any\)
* Cookies \(if any\)
* Headers

### Exception handler page

To configure a custom error handling page for the Production environment, use the Exception Handling Middleware. The middleware:

* Catches and logs exceptions.
* Re-executes the request in an alternate pipeline for the page or controller indicated. The request isn't re-executed if the response has started.

In the following example, UseExceptionHandler adds the Exception Handling Middleware in non-Development environments:

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}
```

#### Access the exception

Use IExceptionHandlerPathFeature to access the exception and the original request path in an error handler controller or page:

```csharp
var exceptionHandlerPathFeature =
    HttpContext.Features.Get<IExceptionHandlerPathFeature>();
if (exceptionHandlerPathFeature?.Error is FileNotFoundException)
{
    ExceptionMessage = "File error thrown";
}
if (exceptionHandlerPathFeature?.Path == "/index")
{
    ExceptionMessage += " from home page";
}
```

### Exception handler lambda

An alternative to a custom exception handler page is to provide a lambda to UseExceptionHandler. Using a lambda allows access to the error before returning the response.

Here's an example of using a lambda for exception handling:

```csharp
app.UseExceptionHandler(errorApp =>
   {
        errorApp.Run(async context =>
        {
            context.Response.StatusCode = 500;
            context.Response.ContentType = "text/html";

            await context.Response.WriteAsync("<html lang=\"en\"><body>\r\n");

            var exceptionHandlerPathFeature = 
                context.Features.Get<IExceptionHandlerPathFeature>();

            if (exceptionHandlerPathFeature?.Error is FileNotFoundException)
                await context.Response.WriteAsync("File error thrown!<br><br>\r\n");

            await context.Response.WriteAsync("<a href=\"/\">Home</a><br>\r\n");
        });
    });
```

### UseStatusCodePages

By default, an ASP.NET Core app doesn't provide a status code page for HTTP status codes, such as 404 - Not Found. The app returns a status code and an empty response body. To provide status code pages, use Status Code Pages middleware.

The middleware is made available by the Microsoft.AspNetCore.Diagnostics package, which is in the Microsoft.AspNetCore.App metapackage.

To enable default text-only handlers for common error status codes, call UseStatusCodePages in the Startup.Configure method: `app.UseStatusCodePages();`

Call `UseStatusCodePages` before request handling middleware \(for example, Static File Middleware and MVC Middleware\). Here's an example of text displayed by the default handlers:

`Status Code: 404; Not Found`

### Exception-handling code

Code in exception handling pages can throw exceptions. It's often a good idea for production error pages to consist of purely static content.

Once the headers for a response are sent:

* The app can't change the response's status code.
* Any exception pages or handlers can't run. The response must be completed or the connection aborted.

### Server exception handling

In addition to the exception handling logic in your app, the HTTP server implementation can handle some exceptions. If the server catches an exception before response headers are sent, the server sends a 500 - Internal Server Error response without a response body. If the server catches an exception after response headers are sent, the server closes the connection. Requests that aren't handled by your app are handled by the server. Any exception that occurs when the server is handling the request is handled by the server's exception handling. The app's custom error pages, exception handling middleware, and filters don't affect this behavior.

### Startup exception handling

Only the hosting layer can handle exceptions that take place during app startup. The host can be configured to capture startup errors and capture detailed errors.

The hosting layer can show an error page for a captured startup error only if the error occurs after host address/port binding. If binding fails:

* The hosting layer logs a critical exception.
* The dotnet process crashes.
* No error page is displayed when the HTTP server is Kestrel.

### Exception filters

In MVC apps, exception filters can be configured globally or on a per-controller or per-action basis. In Razor Pages apps, they can be configured globally or per page model. These filters handle any unhandled exception that occurs during the execution of a controller action or another filter. 

{% hint style="success" %}
Exception filters are useful for trapping exceptions that occur within MVC actions, but they're not as flexible as the Exception Handling Middleware. Recommend using the middleware. Use filters only where you need to perform error handling differently based on which MVC action is chosen.
{% endhint %}

