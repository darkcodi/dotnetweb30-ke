# CSRF/XSRF protection

### ASP.NET Core antiforgery configuration <a id="aspnet-core-antiforgery-configuration"></a>

ASP.NET Core implements antiforgery using **ASP.NET Core Data Protection**.

In ASP.NET Core 2.0 or later, the **FormTagHelper** injects antiforgery tokens into HTML form elements. **Razor Pages** are automatically protected from XSRF/CSRF.

Customize antiforgery options in `Startup.ConfigureServices`:

```csharp
services.AddAntiforgery(options => 
{
    // Set Cookie properties using CookieBuilder properties†.
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.SuppressXFrameOptionsHeader = false;
});
```

### Defending against CSRF

The most common approach to defending against CSRF attacks is to use the _Synchronizer Token Pattern_ \(STP\). STP is used when the user requests a page with form data:

1. The server sends a token associated with the current user's identity to the client.
2. The client sends back the token to the server for verification.
3. If the server receives a token that doesn't match the authenticated user's identity, the request is rejected.

Here is an example of how to explicitly add an antiforgery token:

```aspnet
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

The `ValidateAntiForgeryToken` attribute requires a token for requests to the action methods it decorates, including HTTP GET requests. Requests made to actions that have this filter applied are blocked unless the request includes a valid antiforgery token:

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> TransferMoney(TransferMoneyModel model)
{
    ...
}
```

Instead of broadly applying the `ValidateAntiForgeryToken` attribute and then overriding it with `IgnoreAntiforgeryToken` attributes, the `AutoValidateAntiforgeryToken` attribute can be used. This attribute works identically to the `ValidateAntiForgeryToken` attribute, except that it doesn't require tokens for requests made using the following HTTP methods: 

* GET
* HEAD
* OPTIONS
* TRACE

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
    ...
}
```

