# Query data sources by using EF

You can build and execute queries using Entity Framework \(EF\) to fetch the data from the underlying database.

Entity framework supports **three types** of queries:

1. LINQ-to-Entities,
2. Entity SQL,
3. Native SQL.

### LINQ-to-Entities

You can use the LINQ method syntax or query syntax when querying with EDM.

The following sample LINQ-to-Entities query fetches the data from the `Student` table in the database.

**LINQ Method syntax:**

```csharp
//Querying with LINQ to Entities 
using (var context = new SchoolDBEntities())
{
    var query = context.Students
                       .where(s => s.StudentName == "Bill")
                       .FirstOrDefault<Student>();
}
```

**LINQ Query syntax:**

```csharp
using (var context = new SchoolDBEntities())
{
    var query = from st in context.Students
                where st.StudentName == "Bill"
                select st;
   
    var student = query.FirstOrDefault<Student>();
}
```

### Entity SQL

Entity SQL is another way to create a query. It is processed by the Entity Framework's Object Services directly. It returns `ObjectQuery` instead of `IQueryable`.

You need an `ObjectContext` to create a query using Entity SQL.

```csharp
//Querying with Object Services and Entity SQL
string sqlString = "SELECT VALUE st FROM SchoolDBEntities.Students " +
                    "AS st WHERE st.StudentName == 'Bill'";
    
var objctx = (ctx as IObjectContextAdapter).ObjectContext;
                
ObjectQuery<Student> student = objctx.CreateQuery<Student>(sqlString);
Student newStudent = student.First<Student>();
```

### Native SQL

You can execute native SQL queries for a relational database, as shown below:

```csharp
using (var ctx = new SchoolDBEntities())
{
    var studentName = ctx.Students.SqlQuery("Select studentid, studentname, standardId from Student where studentname='Bill'").FirstOrDefault<Student>();
}    
```

