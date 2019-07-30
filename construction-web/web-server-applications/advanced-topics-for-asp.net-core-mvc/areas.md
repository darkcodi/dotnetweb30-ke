# Areas

Areas are an ASP.NET feature used to organize related functionality into a group as a separate namespace \(for routing\) and folder structure \(for views\). Using areas creates a hierarchy for the purpose of routing by adding another route parameter, `area`, to `controller` and `action` or a Razor Page `page`.

Controllers decorated with the `[Area]` attribute to associate the controller with the area:

```csharp
[Area("Products")]
public class ManageController : Controller
{
```

The area route added to startup:

```csharp
app.UseMvc(routes =>
{
    routes.MapRoute(
      name: "MyArea",
      template: "{area:exists}/{controller=Home}/{action=Index}/{id?}");

    routes.MapRoute(
       name: "default",
       template: "{controller=Home}/{action=Index}/{id?}");
});
```

