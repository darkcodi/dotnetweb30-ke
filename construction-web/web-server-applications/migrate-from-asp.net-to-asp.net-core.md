# Migrate from ASP.NET to ASP.NET Core

### 1. Create the ASP.NET Core project

Create a **new** _**empty**_ ASP.NET Core web app **with the same name** as the previous project so the namespaces in the two projects match. Having the same namespace makes it easier to copy code between the two projects. You'll have to create this project in a different directory than the previous project to use the same name.

### 2. Configure the site to use MVC <a id="configure-the-site-to-use-mvc"></a>

When targeting .NET Core, the `Microsoft.AspNetCore.App` metapackage is referenced by default. This package contains packages commonly used packages by MVC apps.

Open the _Startup.cs_ file and change the code to match the following:

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        // ...

        app.UseMvc(routes =>
        {
            routes.MapRoute(
                name: "default",
                template: "{controller=Home}/{action=Index}/{id?}");
        });
    }
}
```

### 3. Add controllers and views <a id="add-a-controller-and-view"></a>

* Copy each of the methods from the ASP.NET MVC `HomeController` to the new `HomeController`.
* Copy the _About.cshtml_, _Contact.cshtml_, and _Index.cshtml_ Razor view files from the ASP.NET MVC project to the ASP.NET Core project.

### 4. Copy static content

In previous versions of ASP.NET MVC, **static content was hosted from the root** of the web project and was intermixed with server-side files. In ASP.NET Core, **static content is hosted in the** _**wwwroot**_ **folder**.

* Copy the static content from your old ASP.NET MVC app to the _wwwroot_ folder in your ASP.NET Core project.
* Copy the _favicon.ico_ file from the old MVC project to the _wwwroot_ folder in the ASP.NET Core project.

### 5. Migrate the layout file

* Copy the _\_ViewStart.cshtml_ file from the old ASP.NET MVC project's _Views_ folder into the ASP.NET Core project's _Views_ folder.
* \[OPTIONAL\] Copy _\_ViewImports.cshtml_ from the _FullAspNetCore_ MVC project's _Views_ folder into the ASP.NET Core project's _Views_ folder. Remove any namespace declaration in the _\_ViewImports.cshtml_ file.
* Copy the _\_Layout.cshtml_ file from the old ASP.NET MVC project's _Views/Shared_ folder into the ASP.NET Core project's _Views/Shared_ folder.

Open _\_Layout.cshtml_ file and make the following changes \(the completed code is shown below\):

* Replace `@Styles.Render("~/Content/css")` with a `<link>` element to load _bootstrap.css_ \(see below\).
* Remove `@Scripts.Render("~/bundles/modernizr")`.
* Comment out the `@Html.Partial("_LoginPartial")` line \(surround the line with `@*...*@`\).
* Replace `@Scripts.Render("~/bundles/jquery")` with a `<script>` element.
* Replace `@Scripts.Render("~/bundles/bootstrap")` with a `<script>` element.

### 6. Solve HTTP 500 errors <a id="solve-http-500-errors"></a>

There are many problems that can cause a HTTP 500 error message that contain no information on the source of the problem, therefore it's good to configure developer exception page.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    
    // ...
}
```

