# DDL, DML, DCL understanding

### **DDL \(Data Definition Language\)**

DDL actually consists of the SQL commands that can be used to define the database schema. It simply deals with descriptions of the database schema and is used to create and modify the structure of database objects in database.

**Examples of DDL commands:**

* **CREATE** – is used to create the database or its objects \(like table, index, function, views, store procedure and triggers\).
* **DROP** – is used to delete objects from the database.
* **ALTER** – is used to alter the structure of the database.
* **TRUNCATE** – is used to remove all records from a table, including all spaces allocated for the records are removed.
* **COMMENT** – is used to add comments to the data dictionary.
* **RENAME** – is used to rename an object existing in the database.

### **DML \(Data Manipulation Language\)**

The SQL commands that deals with the manipulation of data present in database belong to DML or Data Manipulation Language and this includes most of the SQL statements.

**Examples of DML:**

* **SELECT** – is used to retrieve data from the a database.
* **INSERT** – is used to insert data into a table.
* **UPDATE** – is used to update existing data within a table.
* **DELETE** – is used to delete records from a database table.

### **DCL \(Data Control Language\)**

DCL includes commands such as GRANT and REVOKE which mainly deals with the rights, permissions and other controls of the database system.

**Examples of DCL commands:**

* **GRANT** – gives user’s access privileges to database.
* **REVOKE** – withdraw user’s access privileges given by using the GRANT command.

### **TCL \(Transaction Control Language\)**

TCL commands deals with the transaction within the database.

**Examples of TCL commands:**

* **COMMIT** – commits a Transaction.
* **ROLLBACK** – rollbacks a transaction in case of any error occurs.
* **SAVEPOINT** – sets a savepoint within a transaction.
* **SET TRANSACTION** – specify characteristics for the transaction.

