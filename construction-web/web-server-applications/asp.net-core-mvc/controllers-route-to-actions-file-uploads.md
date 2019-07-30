# Controllers \(Route to actions, File uploads\)

### Routing

_ASP.NET Core MVC_ is built on top of _ASP.NET Core's_ routing, a powerful URL-mapping component that lets you build applications that have comprehensible and searchable URLs.

**Convention-based routing** enables you to globally define the URL formats that your application accepts and how each of those formats maps to a specific action method on given controller. 

```csharp
routes.MapRoute(name: "Default", template: "{controller=Home}/{action=Index}/{id?}");
```

**Attribute routing** enables you to specify routing information by decorating your controllers and actions with attributes that define your application's routes.

```csharp
[Route("api/[controller]")]
public class ProductsController : Controller
{
  [HttpGet("{id}")]
  public IActionResult GetProduct(int id)
  {
    // ...
  }
}
```

### File uploads

To upload small files, you can use a multi-part HTML form or construct a POST request using JavaScript. An example form using Razor, which supports multiple uploaded files, is shown below:

```aspnet
<form method="post" enctype="multipart/form-data" asp-controller="UploadFiles" asp-action="Index">
    <div class="form-group">
        <div class="col-md-10">
            <p>Upload one or more files using this form:</p>
            <input type="file" name="files" multiple>
        </div>
    </div>
    <div class="form-group">
        <div class="col-md-10">
            <input type="submit" value="Upload">
        </div>
    </div>
</form>
```

When uploading files using model binding and the `IFormFile` interface, the action method can accept either a single `IFormFile` or an `IEnumerable<IFormFile>` \(or `List<IFormFile>`\) representing several files. 

```csharp
[HttpPost("UploadFiles")]
public async Task<IActionResult> Post(List<IFormFile> files)
{
    // full path to file in temp location
    var filePath = Path.GetTempFileName();

    foreach (var formFile in files)
    {
        using (var stream = new FileStream(filePath, FileMode.Create))
        {
            await formFile.CopyToAsync(stream);
        }
    }

    return Ok(new { count = files.Count, filePath});
}
```

