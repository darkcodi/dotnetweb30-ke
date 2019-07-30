# Configuration

ASP.NET Core supports many methods of configuration. In ASP.NET Core application, the configuration is stored in name-value pairs and it can be read at runtime from various parts of the application. The name-value pairs may be grouped into multi-level hierarchy. The application configuration data may come from

* File, such as JSON, XML, INI
* Environment variables
* Command
* Line arguments 
* An in-memory collection
* Custom providers

Configuration System in ASP.NET Core is restructured from the older version of ASP.NET. The older version uses "System.Configuration" namespace and is able to read XML configuration file such as web.config. The new configuration model can be accessed to the key/value based settings and it can retrieve various sources, such as JSON, XML and INI.

### Example of reading configuration using JSON provider

Generally, configuration remains in simple key/value structure or might in hierarchical structure when using external files. Consider the following `appsetting.json` file for this example.

```csharp
{  
    "status" : "This Status read from appSettings.json file",  
    "ConnectionStrings": {  
        "DefaultConnection": "Server=.\\sqlexpress;Database=Test;Trusted_Connection=True;MultipleActiveResultSets=true"  
    }  
}
```

The `AddJsonFile` method of `JsonConfigurationExtensions` class is used to JSON file to builder. We can get simple configuration value by using key name. If configuration value is in hierarchical structure, it can be retrieved using a `:` seperated key, starting from root of the hierarchy. In this example, if we want to get value for `DefaultConnection`, then the key becomes `ConnectionStrings:DefaultConnection`.

```csharp
public class Startup 
{  
        public IConfiguration Configuration { get; set; }  
        public Startup() 
        {   
         var builder = new ConfigurationBuilder()     
            .AddJsonFile("appSettings.json");   
         Configuration = builder.Build();   
        }   
         
        public void ConfigureServices(IServiceCollection services)  
        {             
            services.AddMvc();  
        } 
         
        public void Configure(IApplicationBuilder app)
        {  
            app.UseMvc();     
            app.Run(context => {  
                var status = Configuration["status"];   
                var connectionString = Configuration["ConnectionStrings:DefaultConnection"];   
            });   
        }  
}
```

### Retrieve Configuration Data at controller

In the above mentioned example, I am retrieving the configuration value in startup class itself. The new version of ASP.NET has built-in support for dependency injection. Using DI, we can inject the value of configuration to the Controller.

Using `AddSingleton` method of `ServiceCollectionServiceExtensions` class, we can add a singleton service of the specified type with an instance of service.

{% code-tabs %}
{% code-tabs-item title="Startup.cs" %}
```csharp
public void ConfigureServices(IServiceCollection services)  
{             
            services.AddMvc();  
            services.AddSingleton<IConfiguration>(Configuration);  
} 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="HomeController.cs" %}
```csharp
public class HomeController : Controller  
{  
    IConfiguration _configuration;  
    public HomeController(IConfiguration configuration)  
    {  
        _configuration = configuration;  
    }  
    
    [Route("home/index")]  
    public IActionResult Index()  
    {  
        ViewBag.connectionstring = _configuration["ConnectionStrings:DefaultConnection"];  
        return View();  
    }  
} 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Get Configuration object using options pattern

The Options pattern enables us to use custom option classes to represent a group of related settings. The Option class must have public read-write property that is defined for each setting and the class must not take any parameters. The `Microsoft.Extensions.Options.ConfigurationExtensions` dependency contains the extension method for `IServiceCollection.Configure`.

Here, I have defined my model and I am using same `appsetting.json` that was used in previous example. In this example, I have bound the connection string setting of `appsetting.json` with my model class.

```csharp
public class ConnectionString   
{  
    public ConnectionString()  {  }  
    public string DefaultConnection { get; set; }  
    public string MainDBConnectionString { get; set; }  
} 
```

In the following code, `IConfigureOptions` service is added to the Service Container. It binds `ConnectionStrings` class to the section `ConnectionStrings` of the `appsettings.json` file.

{% code-tabs %}
{% code-tabs-item title="Startup.cs" %}
```csharp
public void ConfigureServices(IServiceCollection services)  
{              
    services.AddOptions();  
      
    //Configure Option using Extensions method  
    services.Configure<ConnectionString>(Configuration.GetSection("ConnectionStrings"));  
      
    services.AddSingleton<IConfiguration>(Configuration);  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Working with In-memory provider

The new configuration framework of ASP.NET Core does also support in-memory configuration. In this type of configuration, the values are directly stored into the code and the later part of application uses this configuration. Following is a sample that shows how to use the in-memory provider and bind to a class.

```csharp
public Startup()  
{  
        var builder = new ConfigurationBuilder();  
  
        var dic = new Dictionary<string, string>  
        {  
            {"Profile:FirstName", "Jignesh"},  
            {"Profile:LastName", "Trivedi"},  
            {"Profile:Designation", "PL"}  
        };  
        builder.AddInMemoryCollection(dic);  
        Configuration = builder.Build();  
}
```

Using `Configuration["Profile:FirstName"]`, we can get the value of firstname of profile configuration. We can also bind this value with custom model. Her,e I have created the following “Profile” class to bind this profile value.

```csharp
public class Profile  
{  
    public string FirstName { get; set;}  
    public string LastName { get; set;}  
    public string Designation { get; set;}  
} 
```

The following sample shows how to bind to a profile and use the options pattern with ASP.NET Core MVC application.

{% code-tabs %}
{% code-tabs-item title="Startup.cs " %}
```csharp
public void ConfigureServices(IServiceCollection services)  
{  
    services.AddOptions();  
    services.Configure<Profile>(Configuration.GetSection("Profile"));  
    services.AddMvc();  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="HomeController.cs" %}
```csharp
public class HomeController : Controller  
{  
    Profile _profile;  
    public HomeController(IOptions<Profile> Profile)  
    {  
        _profile = Profile.Value;  
    }  
    [Route("home/index")]  
    public IActionResult Index()  
    {  
        ViewBag.FirstName = _profile.FirstName;  
        return View();  
    }  
} 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

