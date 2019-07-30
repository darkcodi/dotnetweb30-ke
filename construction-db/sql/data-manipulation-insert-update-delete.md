# Data manipulation \(insert, update, delete\)

### INSERT: Populating Tables with Data

The INSERT statement is used to add rows to a table, either directly or through an updateable view. The syntax differs slightly among SQL99, Oracle 9i, DB2 UDB 8.1, and MS SQL Server 2000, but it is possible to come up with some kind of a generic INSERT syntax that works with all our "big three" databases:

```sql
INSERT INTO <table_or_view_name>
[(<column_name>,...)]
{ {VALUES (<literal> |
           <expression> |
           NULL |
           DEFAULT,...)} |
  {<select_statement>} }
```

### UPDATE: Modifying Table Data

The UPDATE statement serves the purpose of modifying existing database information. Here is the generic syntax for our "big three" databases:

```sql
UPDATE <table_or_view_name>
SET {<column_name> = <literal> |
                     <expression> |
                     (<single_row_select_statement>) |
                   NULL |
                   DEFAULT,...}
[WHERE <predicate>]
```

### DELETE: Removing Data from Table

The DELETE statement removes rows from a single table \(either directly or through an updateable view\). The generalized syntax is:

```sql
DELETE FROM <table_or_view_name>
WHERE <predicate>
```

