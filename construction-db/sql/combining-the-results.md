# Combining the results of multiple queries \(UNION, EXCEPT, INTERSECT, MINUS, subqueries\)

### UNION

{% hint style="success" %}
**Combines the results** of two or more queries into a single result set. This set includes all the rows that belong to all queries in the union.
{% endhint %}

The UNION operation is different from using joins that combine columns from two tables.

#### Limitations

* Each SELECT statement within UNION must have the same number of columns
* The columns must also have similar data types
* The columns in each SELECT statement must also be in the same order

#### UNION syntax

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

#### UNION ALL Syntax

```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

### EXCEPT/INTERSECT

{% hint style="success" %}
**EXCEPT** returns distinct rows from the left input query that aren't output by the right input query.
{% endhint %}

{% hint style="success" %}
**INTERSECT** returns distinct rows that are output by both the left and right input queries operator.
{% endhint %}

#### Syntax

```sql
{ <query_specification> | ( <query_expression> ) }
{ EXCEPT | INTERSECT }
{ <query_specification> | ( <query_expression> ) }
```

#### Examples

```sql
SELECT ProductID
FROM Production.Product
INTERSECT
SELECT ProductID
FROM Production.WorkOrder;
--Result: products that have work orders
```

```sql
SELECT ProductID
FROM Production.Product
EXCEPT
SELECT ProductID
FROM Production.WorkOrder;
--Result: products without work orders
```

### MINUS

{% hint style="success" %}
**MINUS** operator is used to return all rows in the first SELECT statement that are not returned by the second SELECT statement.
{% endhint %}

Each SELECT statement will define a dataset. The MINUS operator will retrieve all records from the first dataset and then remove from the results all records from the second dataset.

{% hint style="info" %}
**TIP:** The MINUS operator is not supported in all SQL databases. It can used in databases such as Oracle.

For databases such as SQL Server, PostgreSQL, and SQLite, use the **EXCEPT** operator to perform this type of query.
{% endhint %}

#### Syntax

```sql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
MINUS
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

### Subqueries

{% hint style="success" %}
A **subquery** is a query that is nested inside a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement, or inside another subquery.
{% endhint %}

A subquery can be used anywhere an expression is allowed.

#### Restrictions

A subquery is subject to the following restrictions:

* The select list of a subquery introduced with a comparison operator can include only one expression or column name.
* If the `WHERE` clause of an outer query includes a column name, it must be join-compatible with the column in the subquery select list.
* The **ntext**, **text**, and **image** data types cannot be used in the select list of subqueries.
* The `DISTINCT` keyword cannot be used with subqueries that include GROUP BY.
* The `COMPUTE` and `INTO` clauses cannot be specified.
* `ORDER BY` can only be specified when `TOP` is also specified.
* A view created by using a subquery cannot be updated.
* The select list of a subquery introduced with `EXISTS`, by convention, has an asterisk \(\*\) instead of a single column name. 

#### Example

```sql
SELECT Ord.SalesOrderID, Ord.OrderDate,
    (SELECT MAX(OrdDet.UnitPrice)
     FROM Sales.SalesOrderDetail AS OrdDet
     WHERE Ord.SalesOrderID = OrdDet.SalesOrderID) AS MaxUnitPrice
FROM Sales.SalesOrderHeader AS Ord;
```

