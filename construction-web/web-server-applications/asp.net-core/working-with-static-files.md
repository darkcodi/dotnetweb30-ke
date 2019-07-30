# Working with Static Files

Static files, such as HTML, CSS, images, and JavaScript, are assets an ASP.NET Core app serves directly to clients.

Static files are stored within the project's web root directory. The default directory is _&lt;content\_root&gt;/wwwroot_, but it can be changed via the `UseWebRoot` method.

### Serve files inside of web root

Static files are accessible via a path relative to the web root. For example, the **Web Application** project template contains several folders within the _wwwroot_ folder:

* **wwwroot**
  * **css**
  * **images**
  * **js**

Invoke the `UseStaticFiles` method within `Startup.Configure`:

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();
}
```

### Serve files outside of web root

Consider a directory hierarchy in which the static files to be served reside outside of the web root:

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles(); // For the wwwroot folder

    app.UseStaticFiles(new StaticFileOptions
    {
        FileProvider = new PhysicalFileProvider(
            Path.Combine(Directory.GetCurrentDirectory(), "MyStaticFiles")),
        RequestPath = "/StaticFiles"
    });
}
```

### Static file authorization <a id="static-file-authorization"></a>

The Static File Middleware doesn't provide authorization checks. Any files served by it, including those under _wwwroot_, are publicly accessible. To serve files based on authorization:

* Store them outside of _wwwroot_ and any directory accessible to the Static File Middleware.
* Serve them via an action method to which authorization is applied. Return a `FileResult` object.

```csharp
[Authorize]
public IActionResult BannerImage()
{
    var file = Path.Combine(Directory.GetCurrentDirectory(), 
                            "MyStaticFiles", "images", "banner1.svg");

    return PhysicalFile(file, "image/svg+xml");
}
```

### Non-standard content types <a id="non-standard-content-types"></a>

Static File Middleware understands almost 400 known file content types. If the user requests a file with an unknown file type, Static File Middleware passes the request to the next middleware in the pipeline. If no middleware handles the request, a _404 Not Found_ response is returned. 

The following code enables serving unknown types and renders the unknown file as an image:

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles(new StaticFileOptions
    {
        ServeUnknownFileTypes = true,
        DefaultContentType = "image/png"
    });
}
```

