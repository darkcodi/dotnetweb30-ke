# Joins understanding

There are four basic types of SQL joins: inner, left, right, and full.

* **\(INNER\) JOIN**: Select all records from Table A and Table B, where the join condition is met.
* **LEFT \(OUTER\) JOIN**: Select all records from Table A, along with records from Table B for which the join condition is met \(if at all\).
* **RIGHT \(OUTER\) JOIN**: Select all records from Table B, along with records from Table A for which the join condition is met \(if at all\).
* **FULL \(OUTER\) JOIN**: Select all records from Table A and Table B, regardless of whether the join condition is met or not.

The easiest and most intuitive way to explain the difference between these four types is by using a Venn diagram, which shows all possible logical relations between data sets.

![](../../.gitbook/assets/joins.png)

