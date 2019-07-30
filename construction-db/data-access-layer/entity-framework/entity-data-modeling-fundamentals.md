# Entity Data Modeling Fundamentals

### Creating a Model

Entity Framework uses a set of conventions to build a model based on the shape of your entity classes. You can specify additional configuration to supplement and/or override what was discovered by convention.

#### Use fluent API to configure a model

You can override the `OnModelCreating` method in your derived context and use the `ModelBuilder API` to configure your model. This is the most powerful method of configuration and allows configuration to be specified without modifying your entity classes. Fluent API configuration has the highest precedence and will override conventions and data annotations.

```csharp
using Microsoft.EntityFrameworkCore;

namespace EFModeling.Configuring.FluentAPI.Samples.Required
{
    class MyContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Blog>()
                .Property(b => b.Url)
                .IsRequired();
        }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }
    }
}
```

#### Use data annotations to configure a model

You can also apply attributes \(known as Data Annotations\) to your classes and properties. Data annotations will override conventions, but will be overridden by Fluent API configuration.

```csharp
using Microsoft.EntityFrameworkCore;
using System.ComponentModel.DataAnnotations;

namespace EFModeling.Configuring.DataAnnotations.Samples.Required
{
    class MyContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        [Required]
        public string Url { get; set; }
    }
}
```

### Including & excluding types/properties

**Including a type/property** in the model means that EF has metadata about that type/property and will attempt to read and write instances from and to the database.

#### Excluding via Data Annotations

```csharp
using Microsoft.EntityFrameworkCore;
using System;
using System.ComponentModel.DataAnnotations.Schema;

namespace EFModeling.Configuring.DataAnnotations.Samples.IgnoreType
{
    class MyContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }

        public BlogMetadata Metadata { get; set; }
    }

    [NotMapped]
    public class BlogMetadata
    {
        public DateTime LoadedFromDatabase { get; set; }
    }
}
```

#### Excluding via Fluent API

```csharp
using Microsoft.EntityFrameworkCore;
using System;

namespace EFModeling.Configuring.FluentAPI.Samples.IgnoreType
{
    class MyContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Ignore<BlogMetadata>();
        }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }

        public BlogMetadata Metadata { get; set; }
    }

    public class BlogMetadata
    {
        public DateTime LoadedFromDatabase { get; set; }
    }
}
```

### Keys

#### Conventions

By convention, a property named `Id` or `<type name>Id` will be configured as the key of an entity.

```csharp
class Car
{
    public string Id { get; set; }

    public string Make { get; set; }
    public string Model { get; set; }
}
```

#### Data Annotations

You can use Data Annotations to configure a single property to be the key of an entity.

```csharp
class Car
{
    [Key]
    public string LicensePlate { get; set; }

    public string Make { get; set; }
    public string Model { get; set; }
}
```

Composite key:

```csharp
public class MyTable
{
  [Key, Column(Order = 0)]
  public string SomeId { get; set; }

  [Key, Column(Order = 1)]
  public int OtherId { get; set; }
}
```

Foreign key:

```csharp
public class Student
{
    public int StudentID { get; set; }
    public string StudentName { get; set; }
        
    [ForeignKey("Standard")]
    public int StandardRefId { get; set; }
    public Standard Standard { get; set; }
}
```

### Modeling a Many-to-Many Relationship

A many-to-many relationship occurs between entities when a one-to-many relationship between them works both ways. A book can appear in many categories and a category can contain many books.

This type of relationship is represented in a database by a _join_ table \(also known among other things as a _bridging_, _junction_ or _linking_ table\).

A many-to-many relationship is defined in code by the inclusion of collection properties in each of the entities - The `Categories` property in the `Book` class, and the `Books` property in the `Category` class:

```csharp
public class Book
{
    public int BookId { get; set; }
    public string Title { get; set; }  
    public Author Author { get; set; }
    public ICollection<Category> Categories { get; set; }
}

public class Category
{
    public int CategoryId { get; set; }
    public string CategoryName { get; set; }
    public ICollection<Book> Books { get; set; }
}
```

The join table will be named after the join entity \(`BookCategory` in this case\) by convention. The relationship also needs to be configured via the Fluent API for EF Core to be able to map it successfully:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<BookCategory>()
        .HasKey(bc => new { bc.BookId, bc.CategoryId });  
    modelBuilder.Entity<BookCategory>()
        .HasOne(bc => bc.Book)
        .WithMany(b => b.BookCategories)
        .HasForeignKey(bc => bc.BookId);  
    modelBuilder.Entity<BookCategory>()
        .HasOne(bc => bc.Category)
        .WithMany(c => c.BookCategories)
        .HasForeignKey(bc => bc.CategoryId);
}
```

