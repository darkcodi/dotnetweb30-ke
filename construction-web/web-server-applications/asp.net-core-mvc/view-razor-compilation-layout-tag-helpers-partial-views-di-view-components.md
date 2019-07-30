# View \(Razor compilation, Layout, Tag Helpers, Partial Views, DI, View components\)

### Razor compilation

A Razor file is compiled at runtime, when the associated Razor Page or MVC view is invoked. Razor files are compiled at both build and publish time using the Razor SDK.

**Build- and publish-time compilation** of Razor files is enabled by default by the Razor SDK. Editing Razor files after they're updated is supported at build time. By default, only the compiled _Views.dll_and no _.cshtml_ files or references assemblies required to compile Razor files are deployed with your app.

Build-time compilation is supplemented by **runtime compilation** of Razor files. ASP.NET Core MVC will recompile Razor files when the contents of a _.cshtml_ file change.

### Layout

Pages and views frequently share visual and programmatic elements.

Most web apps have a common layout that provides the user with a consistent experience as they navigate from page to page. The layout typically includes common user interface elements such as the app header, navigation or menu elements, and footer.

![](../../../.gitbook/assets/image%20%2880%29.png)

Common HTML structures such as scripts and stylesheets are also frequently used by many pages within an app. All of these **shared elements** may be defined in a _**layout**_ **file**, which can then be referenced by any view used within the app. Layouts reduce duplicate code in views.

By convention, the default layout for an ASP.NET Core app is named _\_Layout.cshtml_. The layout file for new ASP.NET Core projects created with the templates:

![views folder in solutions explorer](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/layout/_static/mvc-web-project-views.png?view=aspnetcore-2.1)

### Tag Helpers

**Tag Helpers** enable server side code to participate in creating and rendering HTML elements in Razor files. You can use tag helpers to **define custom tags** \(for example, `<environment>`\) or to **modify the behavior of existing tags** \(for example, `<label>`\).

The `EnvironmentTagHelper` can be used to include different scripts in your views \(for example, raw or minified\) based on the runtime environment, such as Development, Staging, or Production:

```aspnet
<environment names="Development">
    <script src="~/lib/jquery/dist/jquery.js"></script>
</environment>
<environment names="Staging,Production">
    <script src="https://ajax.aspnetcdn.com/ajax/jquery/jquery-2.1.4.min.js"
            asp-fallback-src="~/lib/jquery/dist/jquery.min.js"
            asp-fallback-test="window.jQuery">
    </script>
</environment>
```

Tag Helpers provide an HTML-friendly development experience and a rich IntelliSense environment for creating HTML and Razor markup. Most of the built-in Tag Helpers target existing HTML elements and provide server-side attributes for the element.

### Partial views

A partial view is a Razor markup file \(_.cshtml_\) that renders HTML output _within_ another markup file's rendered output.

Partial views are an effective way to:

* Break up large markup files into smaller components.
* Reduce the duplication of common markup content across markup files.

Partial views shouldn't be used to maintain common layout elements. Common layout elements should be specified in `_Layout.cshtml` files.

```csharp
public IActionResult OnGetPartial() =>
    new PartialViewResult
    {
        ViewName = "_AuthorPartialRP",
        ViewData = ViewData,
    };
```

There are 2 partial rendering approaches:

* Partial Tag Helper
* Asynchronous HTML Helper

#### Partial Tag Helper <a id="partial-tag-helper"></a>

The Partial Tag Helper renders content asynchronously and uses an HTML-like syntax:

```aspnet
<partial name="_PartialName" />
```

#### Asynchronous/Synchronous HTML Helper <a id="asynchronous-html-helper"></a>

`PartialAsync` returns an `IHtmlContent` type wrapped in a `Task<TResult>`. The method is referenced by prefixing the awaited call with an `@` character:

```csharp
@await Html.PartialAsync("_PartialName")
```

`Partial` and `RenderPartial` are the synchronous equivalents of `PartialAsync` and `RenderPartialAsync`, respectively.

### DI

#### Constructor injection

```csharp
public class HomeController : Controller
{
    private readonly IDateTime _dateTime;

    public HomeController(IDateTime dateTime)
    {
        _dateTime = dateTime;
    }

    public IActionResult Index()
    {
        // ...
    }
}
```

#### Action injection

The `FromServicesAttribute` enables injecting a service directly into an action method without using constructor injection:

```csharp
public IActionResult About([FromServices] IDateTime dateTime)
{
    // ...
}
```

### ViewComponents

**View components** are similar to partial views, but they're much more powerful. View components don't use model binding, and only depend on the data provided when calling into it. This article was written using controllers and views, but view components also work with Razor Pages.

A view component:

* Renders a chunk rather than a whole response.
* Includes the same separation-of-concerns and testability benefits found between a controller and view.
* Can have parameters and business logic.
* Is typically invoked from a layout page.

View components are intended anywhere you have reusable rendering logic that's too complex for a partial view, such as:

* Dynamic navigation menus
* Tag cloud \(where it queries the database\)
* Login panel
* Shopping cart
* Recently published articles
* Sidebar content on a typical blog

```csharp
public class PriorityListViewComponent : ViewComponent
{
    private readonly ToDoContext db;

    public PriorityListViewComponent(ToDoContext context)
    {
        db = context;
    }

    public async Task<IViewComponentResult> InvokeAsync(int maxPriority, bool isDone)
    {
        var items = await GetItemsAsync(maxPriority, isDone);
        return View(items);
    }
    
    private Task<List<TodoItem>> GetItemsAsync(int maxPriority, bool isDone)
    {
        return db.ToDo.Where(x => x.IsDone == isDone &&
                             x.Priority <= maxPriority).ToListAsync();
    }
}
```

Then invoke it in cshtml:

```csharp
@await Component.InvokeAsync("PriorityList", new { maxPriority = 4, isDone = true })
```

