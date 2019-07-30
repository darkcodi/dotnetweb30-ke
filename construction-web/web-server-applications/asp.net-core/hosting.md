# Hosting

### Set up a host

Create a host using an instance of `IWebHostBuilder`. A typical app calls `CreateDefaultBuilder` to start setting up a host:

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

`CreateDefaultBuilder` performs the following tasks:

* **Configures Kestrel** server as the web server using the app's hosting configuration providers.
* **Sets content root** to the path returned by `Directory.GetCurrentDirectory`.
* Loads **host configuration** from:
  * Environment variables prefixed with `ASPNETCORE_` \(for example, `ASPNETCORE_ENVIRONMENT`\).
  * Command-line arguments.
* Loads **app configuration** in the following order from:
  * _appsettings.json_.
  * _appsettings.{Environment}.json_.
  * Secret Manager when the app runs in the `Development` environment using the entry assembly.
  * Environment variables.
  * Command-line arguments.
* **Configures logging** for console and debug output.
* When running behind IIS, enables **IIS Integration**.
* Sets **ServiceProviderOptions.ValidateScopes** to `true` if the app's environment is Development.

When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:

* Scoped services aren't directly or indirectly resolved from the root service provider.
* Scoped services aren't directly or indirectly injected into singletons.

