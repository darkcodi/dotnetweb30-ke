# Model binding and validation

Model binding automates retrieving each of client provided values and converting them from strings to .NET types.

* Retrieves data from various sources such as route data, form fields, and query strings.
* Provides the data to controllers and Razor pages in method parameters and public properties.
* Converts string data to .NET types.
* Updates properties of complex types.

```csharp
[HttpGet("{id}")]
public ActionResult<Pet> GetById(int id, bool dogsOnly)
```

If the default behavior doesn't give the right results, you can use one of the following attributes to specify the source to use for any given target.

* `[FromQuery]` - Gets values from the query string.
* `[FromRoute]` - Gets values from route data.
* `[FromForm]` - Gets values from posted form fields.
* `[FromBody]` - Gets values from the request body.
* `[FromHeader]` - Gets values from HTTP headers.

```csharp
public void OnGet([FromHeader(Name="Accept-Language")] string language)
```

