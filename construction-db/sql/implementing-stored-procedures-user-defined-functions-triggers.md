# Implementing stored procedures, user-defined functions, triggers

### Stored procedures

Stored procedures are linear or sequential programs.

Stored procedures can accept parameters and allow local variable declarations; they are structured and allow the use of submodules; also, they allow repeated and conditional statement execution.

#### Create

```sql
CREATE PROC[EDURE] <procedure_name>
[@<parameter_name> <datatype> [= <default>] [OUTPUT] ], ...
AS
   <procedure_body>
```

#### Remove

```sql
DROP PROCEDURE [qualifier.]<procedure_name>
```

### User-defined Functions

User-defined functions combine the advantages of stored procedures with the capabilities of SQL predefined functions. They can accept parameters, perform specific calculations based on data retrieved by one or more SELECT statement, and return results directly to the calling SQL statement.

#### Create

```sql
CREATE FUNCTION <function_name>
([@<parameter_name> <datatype> [ = <default>]],...)
RETURNS <datatype>
[AS]
BEGIN
   <function_body>
   RETURN <value>
END
```

#### Remove

```sql
DROP FUNCTION [qualifier.]<function_name>
```

### Triggers

A trigger is a special type of stored procedure that fires off automatically whenever a special event in the database occurs. For example, a trigger can be invoked when a row is inserted into a specified table or when certain table columns are being updated.

#### Create

```sql
CREATE TRIGGER <trigger_name>
ON <table_or_view>
{ FOR | AFTER | INSTEAD OF }
{INSERT | UPDATE | DELETE} 
AS 
[IF UPDATE ( <column_name> )
           [AND | OR UPDATE ( <column_name> ) ],...]
<trigger_body>
```

#### Remove

```sql
DROP TRIGGER [qualifier.]<trigger_name>
```

