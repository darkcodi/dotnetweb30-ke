# Aggregations \(ORDER BY, GROUP BY, HAVING, SUM, COUNT, AVG, etc\)

### ORDER BY

{% hint style="success" %}
The ORDER BY keyword is used to **sort the result-set** in ascending or descending order.
{% endhint %}

The ORDER BY keyword sorts the records in ascending order by default.

#### Syntax

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

#### Example

```sql
SELECT * FROM Customers
ORDER BY Country;
```

{% hint style="danger" %}
Columns of type **ntext**, **text**, **image**, **geography**, **geometry**, and **xml** cannot be used in an ORDER BY clause.
{% endhint %}

### GROUP BY

{% hint style="success" %}
The GROUP BY statement **group rows** that have the same values into summary rows
{% endhint %}

It is often used with aggregate functions \(COUNT, MAX, MIN, SUM, AVG\) to group the result-set by one or more columns.

#### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

#### Example

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

#### GROUP BY ROLLUP

Creates a group for each combination of column expressions. In addition, it "rolls up" the results into subtotals and grand totals.

For example, `GROUP BY ROLLUP (col1, col2, col3, col4)` creates groups for each combination of column expressions in the following lists.

* col1, col2, col3, col4
* col1, col2, col3, NULL
* col1, col2, NULL, NULL
* col1, NULL, NULL, NULL
* NULL, NULL, NULL, NULL --This is the grand total

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

#### GROUP BY CUBE <a id="group-by-cube--"></a>

GROUP BY CUBE creates groups for all possible combinations of columns.

For GROUP BY CUBE \(a, b\) the results has groups for unique values of \(a, b\), \(NULL, b\), \(a, NULL\), and \(NULL, NULL\).

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

### HAVING

{% hint style="success" %}
**Specifies a search condition** for a group or an aggregate.
{% endhint %}

The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.

#### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

#### Example

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

### SUM

{% hint style="success" %}
Returns the **sum of all the values**, or only the DISTINCT values, in the expression.
{% endhint %}

SUM can be used with numeric columns only. Null values are ignored.

#### Syntax

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

#### Example

```sql
SELECT Color, SUM(ListPrice)AS TotalList,
       SUM(StandardCost) AS TotalCost
FROM dbo.DimProduct
GROUP BY Color
ORDER BY Color;
```

### COUNT

{% hint style="success" %}
This function returns the **number of items** found in a group. This includes NULL values and duplicates.
{% endhint %}

`COUNT` is a deterministic function when used _**without**_ the OVER and ORDER BY clauses.

#### Syntax

```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

#### Example

```sql
SELECT COUNT(*)
FROM HumanResources.Employee;
```

### AVG

{% hint style="success" %}
This function returns the **average of the values** in a group. It ignores null values.
{% endhint %}

#### Syntax

```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

#### Example

```sql
SELECT AVG(ListPrice)
FROM Production.Product;
```

