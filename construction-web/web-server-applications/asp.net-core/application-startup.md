# Application startup

### Startup class

The `Startup` class \(which is named `Startup` just by convention\) is where:

* The request handling **pipeline is defined** \(`Configure` method\).
* \[OPTIONAL\] **Configured services** required by the app \(`ConfigureServices` method\).

```csharp
public class Startup
{
    // Use this method to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddTransient<ISomeInterface, SomeClass>();
    
        services.AddMvc()
            .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

        services.AddDbContext<MovieContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("MovieDb")));
    }

    // Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
        app.UseHttpsRedirection();
        app.UseStaticFiles();
        app.UseMvc();
    }
}
```

{% hint style="info" %}
Dependency injection works even for **Startup** class!
{% endhint %}

A common use of dependency injection into the `Startup` class is to inject:

* `IHostingEnvironment` to configure services by environment.
* `IConfiguration` to read configuration.
* `ILoggerFactory` to create a logger in `Startup.ConfigureServices`

### Building app's host

The `Startup` class is specified to the app when the app's host is built. The `Startup` class is usually specified by calling the `WebHostBuilderExtensions.UseStartup<TStartup>` method on the host builder:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>();
}
```

{% hint style="info" %}
You can build webhost even **without Startup** class!
{% endhint %}

To configure services and the request processing pipeline without using a `Startup` class, call `ConfigureServices` and `Configure` convenience methods on the host builder.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureServices(services =>
            {
                // ┌( ͝° ͜ʖ͡°)=ε/̵͇̿̿/’̿’̿ ̿    (̿▀̿ ̿Ĺ̯̿̿▀̿ ̿)̄
            })
            .Configure(app =>
            {
                // (╥﹏╥)
            });
}
```

