# EF Core InMemory test

The InMemory provider is useful when you want to test components using something that approximates connecting to the real database, without the overhead of actual database operations.

### InMemory is not a relational database <a id="inmemory-is-not-a-relational-database"></a>

EF Core database providers do not have to be relational databases. InMemory is designed to be a general purpose database for testing, and is not designed to mimic a relational database.

Some examples of this include:

* InMemory will allow you to save data that would violate referential integrity constraints in a relational database.
* If you use DefaultValueSql\(string\) for a property in your model, this is a relational database API and will have no effect when running against InMemory.
* Concurrency via Timestamp/row version \(`[Timestamp]` or `IsRowVersion`\) is not supported. No DbUpdateConcurrencyException will be thrown if an update is done using an old concurrency token.

{% hint style="info" %}
For many test purposes these differences will not matter. However, if you want to test against something that behaves more like a true relational database, then consider using SQLite in-memory mode.
{% endhint %}

### Example testing scenario <a id="example-testing-scenario"></a>

First thing I needed to do was have a constructor that took the OptionsBuilder that I could configure my DbContext options outside of the dbContext itself. This enables us to configure our context to use the InMemory Provider. During the OnConfiguring, check to see if the options have been configured, if not use our default setup.

```csharp
public MyDbContext(string connectionString)
{
    _connectionString = connectionString;
}

public MyDbContext(DbContextOptions<MyDbContext> options) : base(options) { }

protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    if (optionsBuilder.IsConfigured == false)
    {
        optionsBuilder
            .UseMySql(_connectionString)
            .ConfigureWarnings(warnings => warnings.Throw(RelationalEventId.QueryClientEvaluationWarning));    
    }
}
```

### In-Memory Provider

Microsoft provides the [Microsoft.EntityFrameworkCore.InMemory](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.InMemory) NuGet Package that contains the In-Memory provider.

With this package, we now can configure out DbContext to use an in-memory database.

```csharp
var options = new DbContextOptionsBuilder<MyDbContext>()
    .UseInMemoryDatabase(databaseName: "Test")
    // Don't raise the error warning us that the in memory db doesn't support transactions
    .ConfigureWarnings(w => w.Ignore(InMemoryEventId.TransactionIgnoredWarning))
    .Options;

var dbContext = new MyDbContext(options);
```

### SQLite In-Memory

To work around the issue of needing to execute SQL, you may want to check out using the SQLite.

[Microsoft.EntityFrameworkCore.Sqlite](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Sqlite) package provides the provider and is similar to configure.  However, you can configure SQLite connection to be in-memory.  We also will need to make sure the schema is defined using the EnsureCreated.

```csharp
var connection = new SqliteConnection("DataSource=:memory:");
connection.Open();

var options = new DbContextOptionsBuilder<MyDbContext>()
    .UseSqlite(connection)
    .Options;

var dbContext = new MyDbContext(options);
dbContext.Database.EnsureCreated();
```

