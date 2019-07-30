# Creating, modifying, removing database objects

### Tables

#### Create table

```sql
CREATE TABLE <table-name>
    (<column name> <data type>[(<size>)],
    <column name> <data type>[(<size>)],...);
```

#### Alter table

```sql
ALTER TABLE <table name> ADD <column name>
    <data type> <size>;
```

#### Drop table

```sql
DROP TABLE <table name>;
```

### Indexes

#### Create index

```sql
CREATE [UNIQUE] [CLUSTERED | NONCLUSTERED] INDEX <index_name>
ON <table_name> | <view_name> ( column [ ASC | DESC ],...)
[ON filegroup]
```

#### **Rename index**

```sql
ALTER INDEX <index_name>
{[RENAME TO <new_name>] |
 [REBUILD TABLESPACE <tablespace_name>]
};
```

#### Drop index

```sql
DROP INDEX <table_name>.<index_name> [,...]
```

### Views

#### Create view

```sql
CREATE VIEW [[<database_name>.]<owner>.]<view_name>
     [(<column_name>,...)] [WITH {ENCRYPTION | SCHEMABINDING |
     VIEW_METADATA,...}] AS select_statement [WITH CHECK OPTION]
```

#### Alter view

```sql
ALTER VIEW [<qualifier>.]<view_name>
    [(<column_name>,...)] [WITH {ENCRYPTION | SCHEMABINDING |
    VIEW_METADATA}] AS <select_statement> [WITH CHECK OPTION]
```

#### Drop view

```sql
DROP VIEW <view_name> [,...]
```

### Schemas

#### Create schema

```sql
CREATE SCHEMA AUTHORIZATION
    <owner> <create_object_statement>,...
    <grant_privilege_statement>,...
```

#### Drop schema

```sql
DROP SCHEMA <schema_name> RESTRICT
```

