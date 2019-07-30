# Authentication

You can use the `[Authorize]` attribute from `Microsoft.AspNetCore.Authorization` in ASP.NET Core to require a logged-in user for a particular action, or an entire controller. To require authentication for all actions of the `TodoController`, add this attribute above the first line of the controller:

```csharp
[Authorize]
public class TodoController : Controller
{
    // ...
}
```

Try running the application and accessing `/todo` without being logged in. You'll be redirected to the login page automatically.

{% hint style="warning" %}
The `[Authorize]` attribute is actually doing an **authentication** check here, not an authorization check \(despite the name of the attribute\). Later, you'll use the attribute to check both authentication and authorization.
{% endhint %}

