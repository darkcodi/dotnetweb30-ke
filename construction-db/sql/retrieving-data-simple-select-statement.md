# Retrieving data \(simple select statement\)

Here is the generic SELECT statement, as it is defined by the SQL99 standard, for selecting data from a single table.

```sql
SELECT [DISTINCT] [<qualifier>.]<column_name> |
                  * |
                  <expression>
                   [AS <column_alias>],...
FROM  <table_or_view_name> |
      <inline_view>
       [[AS] <table_alias>]
[WHERE <predicate>]
[GROUP BY [<qualifier>.]<column_name>,...
 [HAVING <predicate>]
]
[ORDER_BY <column_name> |
          <column_number>
           [ASC | DESC],...
];
```

### SELECT Clause: What Do We Select?

In the relational databases the SELECT statement selects **values in the columns, literal values, or expressions**. The returned values themselves could be of any valid data types. These values can be displayed in the client application, or written into a file, used in the intermediate calculations, or entered into database tables.

#### Single-column select

```sql
SELECT cust_name_s
FROM   customer
```

#### Multi-column select

```sql
SELECT   cust_id_n,
         cust_status_s,
         cust_name_s
FROM     customer
```

#### **Selecting all columns**

```sql
SELECT *
FROM customer
```

#### **Selecting distinct values**

```sql
SELECT DISTINCT payterms_discpct_n
FROM            payment_terms
```

#### Using literals, functions, and calculated columns

```sql
SELECT SYSDATE
FROM dual
```

```sql
SELECT (5+5)
FROM sysibm.sysdummy1
```

```sql
SELECT cust_name_s,
       100 AS NUMERIC_CONSTANT,
       'ABC' AS STRING_CONSTANT
FROM   customer
```

#### Using subqueries in a SELECT clause

```sql
SELECT prod_num_s,
       prod_price_n,
       (SELECT stax_amt_n
        FROM sales_tax
        WHERE stax_state_s = 'WA') AS TAX_RATE,
FROM    product
```

### FROM Clause: Select from What?

The database objects you should be able to select from are **tables and views**. These come in many flavors — temporary tables, inline views, materialized views, to name just a few — but the truth is that there is nothing else in the RDBMS world to select from.

#### Using aliases in a FROM clause

```sql
SELECT status_id_n,
       s.status_code_s,
       s.status_desc_s
FROM   status s
```

#### Using subqueries in a FROM clause \(inline views\)

```sql
SELECT  cust.id,
        cust.active
FROM    (SELECT cust_id_n AS id,
                cust_status_s AS active,
                cust_name_s,
                cust_alias_s AS alias
         FROM   customer) cust
```

### WHERE Clause: Setting Horizontal Limits

The SQL WHERE clause allows you to limit the number of rows in result sets returned by a query through **specifying some condition or set of conditions**. The search criteria specified in the WHERE clause evaluate to TRUE or FALSE, and all the rules of Boolean algebra are fully applicable there.

#### Using comparison operators

```sql
SELECT cust_name_s
FROM   customer
WHERE  cust_id_n = 7
```

#### Using compound operators: AND, OR

```sql
SELECT  phone_salesmanid_fn
FROM    phone
WHERE   phone_custid_fn IS NULL
        AND phone_type_s = 'PHONE'
```

#### Using the BETWEEN operator

```sql
SELECT  prod_description_s
FROM    product
WHERE   prod_price_n BETWEEN 23.10 AND 30
```

#### Using the IN operator

```sql
SELECT  cust_name_s
FROM    customer
WHERE   cust_alias_s IN
        ('MNGA71396', 'MNGA71398', 'MNGA71400')
```

#### Using the IS NULL operator

```sql
SELECT  phone_salesmanid_fn
FROM    phone
WHERE   phone_custid_fn IS NULL
```

#### Using subqueries in a WHERE clause

```sql
SELECT  ordhdr_nbr_s,
        ordhdr_orderdate_d
FROM    order_header
WHERE   ordhdr_custid_fn =
        (SELECT cust_id_n
         FROM   customer
         WHERE  cust_name_s = 'WILE ELECTRONICS INC.')
```

### GROUP BY and HAVING Clauses: Summarizing Results

**Grouping records** in the result set **based on some criteria** could provide a valuable insight into data that has accumulated in the table.

```sql
SELECT   ordline_ordhdrid_fn,
         SUM(ordline_ordqty_n) AS TOT_QTY_PER_ORDER
FROM     order_line
GROUP BY ordline_ordhdrid_fn
```

The HAVING clause used exclusively with the GROUP BY clause provides a means of additional selectivity.

```sql
SELECT    ordline_ordhdrid_fn,
          SUM(ordline_ordqty_n) TOT_QTY_PER_ORDER
FROM      order_line
GROUP BY  ordline_ordhdrid_fn
HAVING    SUM(ordline_ordqty_n) > 750
```

### ORDER BY Clause: Sorting Query Output

The query returns results matching the criteria unsorted — i.e., in the order they've been found in the table. To **produce sorted output** — alphabetically or numerically — you would use an ORDER BY clause.

```sql
SELECT    cust_name_s,
          cust_alias_s,
          cust_status_s
FROM      customer
ORDER BY  cust_name_s;
```

