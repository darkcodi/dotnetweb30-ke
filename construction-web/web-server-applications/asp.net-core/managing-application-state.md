# Managing Application State

HTTP is a stateless protocol. Without taking additional steps, HTTP requests are independent messages that don't retain user values or app state.

State can be stored using several approaches.

| Storage approach | Storage mechanism |
| :--- | :--- |
| Cookies | HTTP cookies \(may include data stored using server-side app code\) |
| Session state | HTTP cookies and server-side app code |
| TempData | HTTP cookies or session state |
| Query strings | HTTP query strings |
| Hidden fields | HTTP form fields |
| HttpContext.Items | Server-side app code |
| Cache | Server-side app code |
| Dependency Injection | Server-side app code |

### Cookies <a id="cookies"></a>

Cookies store data across requests. Because cookies are sent with every request, their size should be kept to a minimum. Ideally, only an identifier should be stored in a cookie with the data stored by the app. Most browsers restrict cookie size to 4096 bytes. Only a limited number of cookies are available for each domain.

### Session state <a id="session-state"></a>

ASP.NET Core maintains session state by providing a cookie to the client that contains a session ID, which is sent to the app with each request. The app uses the session ID to fetch the session data.

```csharp
services.AddSession(options =>
{
    options.Cookie.Name = ".AdventureWorks.Session";
    options.IdleTimeout = TimeSpan.FromSeconds(10);
    options.Cookie.IsEssential = true;
});
```

### TempData <a id="tempdata"></a>

The cookie-based TempData provider is used by default to store TempData in cookies.

The cookie data is encrypted using `IDataProtector`, encoded with `Base64UrlTextEncoder`, then chunked.

```csharp
services.AddMvc()
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2)
    .AddSessionStateTempDataProvider();

services.AddSession();
```

### Query strings <a id="query-strings"></a>

A limited amount of data can be passed from one request to another by adding it to the new request's query string. This is useful for capturing state in a persistent manner that allows links with embedded state to be shared through email or social networks.

### Hidden fields <a id="hidden-fields"></a>

Data can be saved in hidden form fields and posted back on the next request. This is common in multi-page forms. Because the client can potentially tamper with the data, the app must always revalidate the data stored in hidden fields.

### Cache <a id="cache"></a>

Caching is an efficient way to store and retrieve data. The app can control the lifetime of cached items.

### Dependency Injection <a id="dependency-injection"></a>

Dependency Injection with singleton makes data available to all users:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<MyAppData>();
}
```

