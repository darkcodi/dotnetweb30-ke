# Querying Data

### Basic queries

```csharp
using (var context = new BookStore())
{
    var books = context.Books
        .Where(b => b.Title.Contains("C#"))
        .ToList();
}
```

### Load related data \(joins, include vs thenInclude\)

Entity Framework Core allows you to use the navigation properties in your model to load related entities.

There are three common ORM patterns used to load related data:

1. **Eager loading** means that the related data is loaded from the database as part of the initial query.
2. **Explicit loading** means that the related data is explicitly loaded from the database at a later time.
3. **Lazy loading** means that the related data is transparently loaded from the database when the navigation property is accessed.

#### Joins

```csharp
using (var context = new BloggingContext())
{
   var query = db.Categories         // source
      .Join(db.CategoryMaps,         // target
         c => c.CategoryId,          // FK
         cm => cm.ChildCategoryId,   // PK
         (c, cm) => new { Category = c, CategoryMaps = cm }) // project result
      .Select(x => x.Category);  // select result
}
```

#### Eager loading

You can use the `Include` method to specify related data to be included in query results. In the following example, the blogs that are returned in the results will have their `Posts` property populated with the related posts.

```csharp
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        .Include(blog => blog.Posts)
        .Include(blog => blog.Owner)
        .ToList();
}
```

You can drill down through relationships to include multiple levels of related data using the `ThenInclude` method. The following example loads all blogs, their related posts, and the author of each post.

```csharp
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        .Include(blog => blog.Posts)
            .ThenInclude(post => post.Author)
        .ToList();
}
```

You can chain multiple calls to `ThenInclude` to continue including further levels of related data.

#### Explicit loading

You can explicitly load a navigation property via the `DbContext.Entry(...)` API.

```csharp
using (var context = new BloggingContext())
{
    var blog = context.Blogs
        .Single(b => b.BlogId == 1);

    context.Entry(blog)
        .Collection(b => b.Posts)
        .Load();

    context.Entry(blog)
        .Reference(b => b.Owner)
        .Load();
}
```

#### Lazy loading

{% hint style="info" %}
This feature was introduced in EF Core 2.1
{% endhint %}

The simplest way to use lazy-loading is by installing the `Microsoft.EntityFrameworkCore.Proxies` package and enabling it with a call to `UseLazyLoadingProxies`. For example:

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    => optionsBuilder
        .UseLazyLoadingProxies()
        .UseSqlServer(myConnectionString);
```

### Client vs server query evaluation

Entity Framework Core supports parts of the query being evaluated on the client and parts of it being pushed to the database. It is up to the database provider to determine which parts of the query will be evaluated in the database.

#### Client evaluation

In the following example a helper method is used to standardize URLs for blogs that are returned from a SQL Server database. Because the SQL Server provider has no insight into how this method is implemented, it is not possible to translate it into SQL. All other aspects of the query are evaluated in the database, but passing the returned `URL` through this method is performed on the client.

```csharp
var blogs = context.Blogs
    .OrderByDescending(blog => blog.Rating)
    .Select(blog => new
    {
        Id = blog.BlogId,
        Url = StandardizeUrl(blog.Url)
    })
    .ToList();
```

```csharp
public static string StandardizeUrl(string url)
{
    url = url.ToLower();

    if (!url.StartsWith("http://"))
    {
        url = string.Concat("http://", url);
    }

    return url;
}
```

{% hint style="warning" %}
While client evaluation can be very useful, in some instances it can result in **poor performance**.
{% endhint %}

### Tracking vs. No-Tracking

Tracking behavior controls whether or not Entity Framework Core will keep information about an entity instance in its change tracker. If an entity is tracked, any changes detected in the entity will be persisted to the database during `SaveChanges()`. Entity Framework Core will also fix-up navigation properties between entities that are obtained from a tracking query and entities that were previously loaded into the DbContext instance.

#### Tracking queries

By default, queries that return entity types are tracking. This means you can make changes to those entity instances and have those changes persisted by `SaveChanges()`.

```csharp
using (var context = new BloggingContext())
{
    var blog = context.Blogs.SingleOrDefault(b => b.BlogId == 1);
    blog.Rating = 5;
    context.SaveChanges();
}
```

#### No-tracking queries

No tracking queries are useful when the results are used in a read-only scenario. They are **quicker to execute** because there is no need to setup change tracking information.

```csharp
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        .AsNoTracking()
        .ToList();
}
```

### Raw SQL

Entity Framework Core allows you to drop down to raw SQL queries when working with a relational database. This can be useful if the query you want to perform can't be expressed using LINQ.

```csharp
var blogs = context.Blogs
    .FromSql("SELECT * FROM dbo.Blogs")
    .ToList();
```

You can also pass parameters there:

```csharp
var user = "johndoe";

var blogs = context.Blogs
    .FromSql("EXECUTE dbo.GetMostPopularBlogsForUser {0}", user)
    .ToList();
```

### How query works \(when execution of query performed\)

#### The life of a query

The following is a high level overview of the process each query goes through:

1. The LINQ query is processed by EF Core to build a representation that is ready to be processed by the database provider \(the results are cached\).
2. The result is passed to the database provider, who identifies which parts of the query can be evaluated in the database, translates them to database specific query language and sends to the database.
3. For each item in the result set EF checks if the data represents an entity already in the change tracker \(if needed\).

#### When queries are executed

When you call LINQ operators, you are simply building up an in-memory representation of the query. The query is only sent to the database when the results are consumed.

The most common operations that result in the query being sent to the database are:

* Iterating the results in a `for` loop
* Using an operator such as `ToList`, `ToArray`, `Single`, `Count`
* Databinding the results of a query to a UI

### Tagging Query

{% hint style="info" %}
This feature is new in EF Core 2.2.
{% endhint %}

This feature helps correlate LINQ queries in code with generated SQL queries captured in logs. You annotate a LINQ query using the new `TagWith()` method:

```csharp
  var nearestFriends =
      (from f in context.Friends.TagWith("This is my spatial query!")
      orderby f.Location.Distance(myLocation) descending
      select f).Take(5).ToList();
```

This LINQ query is translated to the following SQL statement:

```sql
-- This is my spatial query!

SELECT TOP(@__p_1) [f].[Name], [f].[Location]
FROM [Friends] AS [f]
ORDER BY [f].[Location].STDistance(@__myLocation_0) DESC
```

It's possible to call `TagWith()` many times on the same query. Query tags are cumulative.

