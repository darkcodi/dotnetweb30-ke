# Logging

ASP.NET Core supports a logging API that works with a variety of built-in and third-party logging providers.

Write logs from anywhere in an app's code by getting an `ILogger` object from DI and calling log methods.

```csharp
public class TodoController : ControllerBase
{
    private readonly ILogger _logger;

    public TodoController(ILogger<TodoController> logger)
    {
        _logger = logger;
    }

    [HttpGet("{id}", Name = "GetTodo")]
    public ActionResult<TodoItem> GetById(string id)
    {
        _logger.LogInformation(LoggingEvents.GetItem, "Getting item {ID}", id);
        // Item lookup code removed.
        if (item == null)
        {
            _logger.LogWarning(LoggingEvents.GetItemNotFound, "GetById({ID}) NOT FOUND", id);
            return NotFound();
        }
        return item;
    }
}
```

For more info see [Implementing logging](../../../construction-core/programming-language/implementing-logging.md).

