# Data modification

Each context instance has a `ChangeTracker` that is responsible for keeping track of changes that need to be written to the database. As you make changes to instances of your entity classes, these changes are recorded in the `ChangeTracker` and then written to the database when you call `SaveChanges`. The database provider is responsible for translating the changes into database-specific operations \(for example, `INSERT`, `UPDATE`, and `DELETE` commands for a relational database\).

### Save data

```csharp
using (var context = new BloggingContext())
{
    var blog = new Blog { Url = "http://sample.com" };
    context.Blogs.Add(blog);
    context.SaveChanges();
}
```

### Related data

If you create several new related entities, adding one of them to the context will cause the others to be added too.

```csharp
using (var context = new BloggingContext())
{
    var blog = new Blog
    {
        Url = "http://blogs.msdn.com/dotnet",
        Posts = new List<Post>
        {
            new Post { Title = "Intro to C#" },
            new Post { Title = "Intro to VB.NET" },
            new Post { Title = "Intro to F#" }
        }
    };

    context.Blogs.Add(blog);
    context.SaveChanges();
}
```

### Cascade delete

Cascade delete is commonly used in database terminology to describe a characteristic that allows the deletion of a row to automatically trigger the deletion of related rows. A closely related concept also covered by EF Core delete behaviors is the automatic deletion of a child entity when it's relationship to a parent has been severed--this is commonly known as "deleting orphans".

#### Optional relationships <a id="optional-relationships"></a>

For optional relationships \(nullable foreign key\) it _is_ possible to save a null foreign key value, which results in the following effects:

| Behavior Name | Effect on dependent/child in memory | Effect on dependent/child in database |
| :--- | :--- | :--- |
| **Cascade** | Entities are deleted | Entities are deleted |
| **ClientSetNull** \(Default\) | Foreign key properties are set to null | None |
| **SetNull** | Foreign key properties are set to null | Foreign key properties are set to null |
| **Restrict** | None | None |

#### Required relationships <a id="required-relationships"></a>

For required relationships \(non-nullable foreign key\) it is _not_ possible to save a null foreign key value, which results in the following effects:

| Behavior Name | Effect on dependent/child in memory | Effect on dependent/child in database |
| :--- | :--- | :--- |
| **Cascade** \(Default\) | Entities are deleted | Entities are deleted |
| **ClientSetNull** | SaveChanges throws | None |
| **SetNull** | SaveChanges throws | SaveChanges throws |
| **Restrict** | None | None |

### Disconnected entities

A DbContext instance will automatically track entities returned from the database.

However, sometimes entities are queried using one context instance and then saved using a different instance. This often happens in "disconnected" scenarios.

#### Attach

The `DbSet.Attach()` method attaches an entire entity graph to the new context with the Unchanged entity state.

```csharp
//disconnected entity graph
Student disconnectedStudent = new Student() { StudentName = "New Student" };
disconnectedStudent.StudentAddress = new StudentAddress() { Address1 = "Address", City = "City1" };

using (var context = new SchoolDBEntities())
{
    context.Students.Attach(disconnectedStudent);
                
    // get DbEntityEntry instance to check the EntityState of specified entity
    var studentEntry = context.Entry(disconnectedStudent);
    var addressEntry = context.Entry(disconnectedStudent.StudentAddress);

    Console.WriteLine("Student: {0}",studentEntry.State);
    Console.WriteLine("StudentAddress: {0}",addressEntry.State);
}
```

