# Application model

Application model include both abstract interfaces and concrete implementation classes that describe an MVC application. This model is the result of MVC discovering the app's controllers, actions, action parameters, routes, and filters according to default conventions

1. ApplicationModel
2. Controllers (ControllerModel)
3. Actions (ActionModel)
4. Parameters (ParameterModel)

![](https://luisfsgoncalves.files.wordpress.com/2015/10/application_model_thumb.png?w=660&h=241)

Each level of the model has access to a common Properties collection, and lower levels can access and overwrite property values set by higher levels in the hierarchy. The properties are persisted to the ActionDescriptor.Properties when the actions are created. Then when a request is being handled, any properties a convention added or modified can be accessed through ActionContext.ActionDescriptor.Properties. Using properties is a great way to configure your filters, model binders, etc. on a per-action basis.

The application model is also created by a set of providers, represented by the IApplicationModelProvider interface.

The application model defines convention abstractions that provide a simpler way to customize the behavior of the models than overriding the entire model or provider. These abstractions are the recommended way to modify your app's behavior. Conventions provide a way for you to write code that will dynamically apply customizations. While filters provide a means of modifying the framework's behavior, customizations let you control how the whole app is wired together.

Application model conventions are applied as options when MVC is added in ConfigureServices in Startup.
```csharp
    public class ApplicationDescription : IApplicationModelConvention
    {
        private readonly string _description;

        public ApplicationDescription(string description)
        {
            _description = description;
        }

        public void Apply(ApplicationModel application)
        {
            application.Properties["description"] = _description;
        }
    }

public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options =>
    {
        options.Conventions.Add(new ApplicationDescription("My Application Description"));
        options.Conventions.Add(new NamespaceRoutingConvention());
        //options.Conventions.Add(new IdsMustBeInRouteParameterModelConvention());
    });
}
```
