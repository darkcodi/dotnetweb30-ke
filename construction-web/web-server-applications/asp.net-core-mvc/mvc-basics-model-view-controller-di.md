# MVC basics \(Model, View, Controller, DI\)

### What is the MVC pattern? <a id="what-is-the-mvc-pattern"></a>

**The Model-View-Controller \(MVC\)** architectural pattern separates an application into three main groups of components: Models, Views, and Controllers. This pattern helps to achieve _separation of concerns_.

Using this pattern, user requests are routed to a Controller which is responsible for working with the Model to perform user actions and/or retrieve results of queries. The Controller chooses the View to display to the user, and provides it with any Model data it requires.

![](../../../.gitbook/assets/image%20%28104%29.png)

{% hint style="info" %}
Both the view and the controller depend on the model. However, the model depends on neither the view nor the controller.
{% endhint %}

### Model

There are two separate model classes that need to be created: a model that represents a to-do item stored in the database \(sometimes called an **entity**\), and the model that will be combined with a view \(the **MV** in MVC\) and sent back to the user's browser. Because both of them can be referred to as "models", the latter one is a **view model**.

Often, the model \(**entity**\) you store in the database is similar but not _exactly_ the same as the model you want to use in MVC \(**the view model**\).

```csharp
public class TodoItem
{
    public Guid Id { get; set; }

    public bool IsDone { get; set; }

    [Required]
    public string Title { get; set; }

    public DateTimeOffset? DueAt { get; set; }
}
```

### View

Views in ASP.NET Core are built using the Razor templating language, which combines HTML and C\# code. Most view code is just HTML, with the occasional C\# statement added in to pull data out of the view model and turn it into text or HTML. The C\# statements are prefixed with the `@` symbol.

```aspnet
@model TodoViewModel
@{
    ViewData["Title"] = "Manage your todo list";
}

<div class="panel panel-default todo-panel">
  <div class="panel-heading">@ViewData["Title"]</div>
  <table class="table table-hover">
      @foreach (var item in Model.Items)
      {
          <tr>
              <td>
                <input type="checkbox" class="done-checkbox">
              </td>
              <td>@item.Title</td>
              <td>@item.DueAt</td>
          </tr>
      }
  </table>
</div>
```

### Controller

Routes that are handled by controllers are called **actions**, and are represented by methods in the controller class.

There are a number of conventions \(common patterns\) used by ASP.NET Core, such as the pattern that `FooController` becomes `/Foo`.

```text
localhost:5000/Home         -> Index()
localhost:5000/Home/About   -> About()
localhost:5000/Home/Contact -> Contact()
```

Action methods can return views, JSON data, or HTTP status codes like `200 OK` and `404 Not Found`. The `IActionResult` return type gives you the flexibility to return any of these from the action.

```csharp
public class TodoController : Controller
{
    public IActionResult Index()
    {
        // Get to-do items from database

        // Put items into a model

        // Render view using the model
    }
}
```

### Dependency Injection

The job of the `ConfigureServices` method is adding things to the **service container**, or the collection of services that ASP.NET Core knows about. Any services you want to use in your application must be added to the service container here in `ConfigureServices`.

```csharp
services.AddSingleton<ISomeService, SomeService>();
```

That's it! When a request comes in and is routed to the `SomeController`, ASP.NET Core will look at the available services and automatically supply the `SomeService` when the controller asks for an `ISomeService`. Because the services are "injected" from the service container, this pattern is called **dependency injection**.

