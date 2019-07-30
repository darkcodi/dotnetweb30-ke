# Dependency Injection

ASP.NET Core supports the **dependency injection \(DI\)** software design pattern, which is a technique for achieving **Inversion of Control \(IoC\)** between classes and their dependencies.

### Registration

Register your dependencies in `ConfigureServices`.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

    services.AddScoped<IMyDependency, MyDependency>();
    services.AddTransient<IOperationTransient, Operation>();
    services.AddScoped<IOperationScoped, Operation>();
    services.AddSingleton<IOperationSingleton, Operation>();
    services.AddSingleton<IOperationSingletonInstance>(new Operation(Guid.Empty));

    // OperationService depends on each of the other Operation types.
    services.AddTransient<OperationService, OperationService>();
}
```

#### Transient <a id="transient"></a>

Transient lifetime services \(`AddTransient`\) are created each time they're requested from the service container. This lifetime works best for lightweight, stateless services.

#### Scoped <a id="scoped"></a>

Scoped lifetime services \(`AddScoped`\) are created once per client request \(connection\).

#### Singleton <a id="singleton"></a>

Singleton lifetime services \(`AddSingleton`\) are created the first time they're requested \(or when `Startup.ConfigureServices` is run and an instance is specified with the service registration\). Every subsequent request uses the same instance.

### Usage

```csharp
public class SomeClass
{
    private readonly IMyDependency _myDependency;

    // injection through constructor
    public SomeClass(IMyDependency myDependency)
    {
        _myDependency = myDependency;
    }
    
    public void DoSomeWork()
    {
        // some logic here that can use _myDependency
    }
}
```

