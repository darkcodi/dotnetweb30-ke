# Strategies for isolating the database in tests

1. Developers should be using isolated databases for development and testing.
2. Tests should be isolated in the data they create and query from other tests.

### Rollback transactions

One popular method is to simply create a transaction at the beginning of a test and roll it back at the end of the test:

```csharp
private ITransaction _tx;

[SetUp]
public void SetUp()
{
    _tx = connection.BeginTransaction();
}

[TearDown]
public void TearDown()
{
    _tx.RollBack();
}
```

In the above pseudo-code, we just make sure we roll back our transaction at the end of the test. We’ll also need to make sure that all of the code executed in our test actually _uses_ this transaction, but that’s really up to your environment how that transaction gets disseminated to your fixtures and so on.

### Drop and recreate database

Another option is to have the database dropped and re-created between each test. This one’s a bit trickier, but not too bad to manage. If you’re already doing database migrations then it’s not too bad to just blast through the scripts to recreate the DB each time around:

```csharp
[SetUp]
public void SetUp()
{
    DatabaseMigrations.Reset();
}

[TearDown]
public void TearDown()
{
}
```

The upside is that you’re wiping the slate clean each time, so you have an absolute known begin state for each test. The downside is that it’s dog slow.

### Delete all data

Just to simply delete all the data. Instead of dropping tables \(slow\), you can just delete data from tables.

### \[BEST\] Use in-memory database for testing

The InMemory provider is useful when you want to test components using something that approximates connecting to the real database, without the overhead of actual database operations.

EF Core database providers do not have to be relational databases. InMemory is designed to be a general purpose database for testing, and is not designed to mimic a relational database.

Some examples of this include:

* InMemory will allow you to save data that would violate referential integrity constraints in a relational database.
* If you use DefaultValueSql\(string\) for a property in your model, this is a relational database API and will have no effect when running against InMemory.
* Concurrency via Timestamp/row version \(`[Timestamp]` or `IsRowVersion`\) is not supported. No DbUpdateConcurrencyException will be thrown if an update is done using an old concurrency token.

