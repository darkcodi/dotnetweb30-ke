# Build command objects and query data from data sources

### DbCommand

You use the **DbCommand** object to send a SQL command to the data store.

`DbCommand` can be a Data Manipulation Language \(DML\) command to retrieve, insert, update, or delete data, as well as Data Definition Language \(DDL\) command, which enables you to create tables and modify schema information at the database.

#### Requirements

The `DbCommand` object requires:

* valid open connection
* valid value for its `CommandText` property
* valid value for its `CommandType` property

#### How to create

* pass a `DbConnection` object into the `DbCommand` object’s constructor
* attach a `DbConnection` object to the existing `DbCommand` object’s `Connection` property
* \(the best way\) use the `CreateCommand` method on the `DbConnection` object

#### Example

```csharp
var nw = ConfigurationManager.ConnectionStrings["nw"];
var connection = new SqlConnection(nw.ConnectionString);
var cmd = connection.CreateCommand();
cmd.CommandType = CommandType.StoredProcedure;
cmd.CommandText = "CustOrderHist";
//don't forget to close the connection!
```

#### Methods

* **ExecuteNonQuery**. Use it when you don’t expect a command to return any rows—an insert, update, or delete query, for example.
* **ExecuteReader**. It returns a `DbDataReader` instance, which is a forward-only, read-only, server-side cursor.
* **ExecuteScalar**. Queries are often expected to return a single row with a single column. In these situations, the results can be treated as a single return value.

