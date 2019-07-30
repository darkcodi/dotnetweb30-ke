# Code First to existing DB

### How-to code-first

* Create database schema
* Create a new project
* Install Entity Framework Core
* Reverse engineer your model
* Register your context with dependency injection

### Reverse engineer your model

Navigate to **Tools –&gt; NuGet Package Manager –&gt; Package Manager Console** then enter:

```text
Scaffold-DbContext "Server=(localdb)\mssqllocaldb;Database=Blogging;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models
```

The reverse engineer process created entity classes \(`Blog.cs` & `Post.cs`\) and a derived context \(`BloggingContext.cs`\) based on the schema of the existing database.

Like this:

```csharp
using System;
using System.Collections.Generic;

namespace EFGetStarted.AspNetCore.ExistingDb.Models
{
    public partial class Blog
    {
        public Blog()
        {
            Post = new HashSet<Post>();
        }

        public int BlogId { get; set; }
        public string Url { get; set; }

        public ICollection<Post> Post { get; set; }
    }
}
```

