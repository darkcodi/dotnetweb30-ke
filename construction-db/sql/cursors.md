# Cursors

SQL Server is a relational database management system \(RDBMS\), and T-SQL is a transactional programming language. This means that it is designed to execute its work in all-or-nothing runs. The database engine is optimized to work in this manner.

Cursors however, like WHILE loops, break away from the transactional nature of T-SQL and allow for programmers to treat each result of a SELECT statement in a certain way by looping through them.

{% hint style="success" %}
In SQL Server the **cursor** is a tool that is used to iterate over a result set, or to loop through each row of a result set one row at a time.
{% endhint %}

#### Example

Step 1: Declare variables to hold the output from the cursor.

```sql
DECLARE @BusinessEntityID as INT;
DECLARE @BusinessName as NVARCHAR(50);
```

Step 2: Declare the cursor object.

```sql
DECLARE @BusinessCursor as CURSOR;
```

Step 3: Assign the query to the cursor.

```sql
SET @BusinessCursor = CURSOR FOR
SELECT BusinessEntityID, Name
 FROM Sales.Store;
```

Step 4: Open the cursor.

```sql
OPEN @BusinessCursor;
```

Step 5: Fetch the first row.

```sql
FETCH NEXT FROM @BusinessCursor INTO @BusinessEntityID, @BusinessName;
```

Step 6: Loop until there are no more results. In the loop print out the ID and the name from the result set and fetch the net row.

```sql
WHILE @@FETCH_STATUS = 0
BEGIN
 PRINT cast(@BusinessEntityID as VARCHAR (50)) + ' ' + @BusinessName;
 FETCH NEXT FROM @BusinessCursor INTO @BusinessEntityID, @BusinessName;
END
```

Step 7: Close the cursor.

```sql
CLOSE @BusinessCursor;
```

Step 8: Deallocate the cursor to free up any memory or open result sets.

```sql
DEALLOCATE @BusinessCursor;
```

