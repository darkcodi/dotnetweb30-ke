# Globalization and localization

**Internationalization** involves _Globalization_ and _Localization_.

**Globalization** is the process of designing apps that support different cultures. Globalization adds support for input, display, and output of a defined set of language scripts that relate to specific geographic areas.

**Localization** is the process of adapting a globalized app, which you have already processed for localizability, to a particular culture/locale.

### Use localization

**`IStringLocalizer`** and **`IStringLocalizer<T>`** were architected to improve productivity when developing localized apps. `IStringLocalizer` uses the `ResourceManager` and `ResourceReader` to provide culture-specific resources at run time. 

```csharp
public class BookController : Controller
{
    private readonly IHtmlLocalizer<BookController> _localizer;

    public BookController(IHtmlLocalizer<BookController> localizer)
    {
        _localizer = localizer;
    }

    public IActionResult Hello(string name)
    {
        ViewData["Message"] = _localizer["<b>Hello</b><i> {0}</i>", name];

        return View();
    }
}
```

A French resource file could contain the following:

| Key | Value |
| :--- | :--- |
| `<i>Hello</i> <b>{0}!</b>` | `<i>Bonjour</i> <b>{0} !</b>` |

{% hint style="info" %}
**Note:** You generally want to only localize text and not HTML.
{% endhint %}

### Configure localization

Localization is configured in the `Startup.ConfigureServices` method:

```csharp
services.AddLocalization(options => options.ResourcesPath = "Resources");

services.AddMvc()
    .AddViewLocalization(LanguageViewLocationExpanderFormat.Suffix)
    .AddDataAnnotationsLocalization();
```

* `AddLocalization` Adds the localization services to the services container. The code above also sets the resources path to "Resources".
* `AddViewLocalization` Adds support for localized view files. In this sample view localization is based on the view file suffix. For example "fr" in the _Index.fr.cshtml_ file.
* `AddDataAnnotationsLocalization` Adds support for localized `DataAnnotations` validation messages through `IStringLocalizer` abstractions.

### Localization middleware

The current culture on a request is set in the localization middleware. The localization middleware is enabled in the `Startup.Configure` method.

```csharp
var supportedCultures = new[]
{
    new CultureInfo("en-US"),
    new CultureInfo("fr"),
};

app.UseRequestLocalization(new RequestLocalizationOptions
{
    DefaultRequestCulture = new RequestCulture("en-US"),
    // Formatting numbers, dates, etc.
    SupportedCultures = supportedCultures,
    // UI strings that we have localized.
    SupportedUICultures = supportedCultures
});
```

