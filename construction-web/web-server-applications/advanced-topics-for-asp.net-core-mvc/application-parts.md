# Application Parts

An Application Part is an abstraction over the resources of an application, from which MVC features like controllers, view components, or tag helpers may be discovered. 

One example of an application part is an AssemblyPart, which encapsulates an assembly reference and exposes types and compilation references 

MVC apps load their features from application parts. In particular, the AssemblyPart class represents an application part that's backed by an assembly. You can use these classes to discover and load MVC features, such as controllers, view components, tag helpers, and razor compilation source

```csharp
// create an assembly part from a class's assembly
var assembly = typeof(Startup).GetTypeInfo().Assembly;
services.AddMvc()
    .AddApplicationPart(assembly);
```

#Application Feature Providers
Application Feature Providers examine application parts and provide features for those parts. There are built-in feature providers for the following MVC features:

    Controllers
    Metadata Reference
    Tag Helpers
    View Components

This sample uses a controller feature provider that runs after the default provider and adds generic controller instances for a specified list of types (defined in EntityTypes.Types):
```csharp
public class GenericControllerFeatureProvider : IApplicationFeatureProvider<ControllerFeature>
{
    public void PopulateFeature(IEnumerable<ApplicationPart> parts, ControllerFeature feature)
    {
        // This is designed to run after the default ControllerTypeProvider, 
        // so the list of 'real' controllers has already been populated.
        foreach (var entityType in EntityTypes.Types)
        {
            var typeName = entityType.Name + "Controller";
            if (!feature.Controllers.Any(t => t.Name == typeName))
            {
                // There's no 'real' controller for this entity, so add the generic version.
                var controllerType = typeof(GenericController<>)
                    .MakeGenericType(entityType.AsType()).GetTypeInfo();
                feature.Controllers.Add(controllerType);
            }
        }
    }
}
```
