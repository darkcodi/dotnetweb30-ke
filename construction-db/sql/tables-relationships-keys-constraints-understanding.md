# Tables, relationships, keys, constraints understanding

### Tables

Tables are the central and the most important objects in any relational database. The primary purpose of any database is to hold data that is logically stored in tables.

{% hint style="info" %}
One of the relational database design principles is that **each table** holds information about **one specific type of thing, or entity**.
{% endhint %}

### Relations

There are several types of database relationships. Today we are going to cover the following:

* One to One Relationships
* One to Many and Many to One Relationships
* Many to Many Relationships
* Self Referencing Relationships

### Keys

#### Super Key

Super key is a **set** of one or more than one keys that can be used to identify a record uniquely in a table. **Example:** Primary key, Unique key, Alternate key are a subset of Super Keys.

#### Candidate Key

Candidate key is a super key from which you cannot remove any fields. There can be multiple Candidate Keys in one table. Each Candidate Key can work as Primary Key.

**Example:** In the below diagram _ID_, _RollNo_ and _EnrollNo_ are Candidate Keys since all these three fields can be work as Primary Key.

#### Primary Key

Primary key is a "main" candidate key. It can not accept null, duplicate values. Only one Candidate Key can be Primary Key.

#### Alternate key

An Alternate key is a key that can be work as a primary key. Basically, it is a Candidate Key that currently is not a Primary Key.

**Example:** In the below diagram _RollNo_ and _EnrollNo_ become Alternate Keys when we define _ID_ as Primary Key.

#### Composite/Compound Key

Composite Key is a combination of more than one fields/columns of a table. It can be a Candidate key, Primary key.

#### Unique Key

It is like Primary key, but it can accept only one null value.

#### Foreign Key

Foreign Key is a field in a database table that is Primary key in another table. It can accept multiple null, duplicate values.

![](../../.gitbook/assets/sqlkeys.png)

### Constraints

Constraints are the rules enforced on the data columns of a table. These are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the database.

The following constraints are commonly used in SQL:

* **NOT NULL** - Ensures that a column cannot have a NULL value
* **UNIQUE** - Ensures that all values in a column are different
* **PRIMARY KEY** - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* **FOREIGN KEY** - Uniquely identifies a row/record in another table
* **CHECK** - Ensures that all values in a column satisfies a specific condition
* **DEFAULT** - Sets a default value for a column when no value is specified
* **INDEX** - Used to create and retrieve data from the database very quickly

