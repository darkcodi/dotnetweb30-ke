# Connect to a data source by using a generic data access interface

ADO.Net Provides consistent access to databases like Microsoft SQL Server, Oracle as well as data sources exposed through OLE DB and XML. Data-sharing consumer applications can use ADO.NET to connect to these data sources and retrieve, manipulate, and update data.

The ADO.NET components have been designed to factor data access from data manipulation. There are two central components of ADO.NET that accomplish this: the DataSet, and the .NET Framework data provider, which is a set of components including the Connection, Command, DataReader and DataAdapter objects.

### Abstracting Data Access

ADO.NET is designed around a set of generic interfaces that abstract the underlying data processing functionality. You can use these interfaces directly to abstract your data access layer so that you can minimize the impact of changing the type of data source that you use. Abstracting data access is extremely helpful when you are designing systems where your customer chooses the database server.

The core interfaces provided by ADO.NET are found in the `System.Data` namespace:

* **IDbConnection** – This is an interface for managing database connections.
* **IDbCommand** – This is an interface for running SQL commands.
* **IDbTransaction** – This is an interface for managing transactions.
* **IDataReader** –This is an interface for reading data returned by a command.
* **IDataAdapter** – This is an interface for channelling data to and from datasets.

### Concrete implementations

The following table shows the provider used to access different types of databases in ADO.NET:

| Database Parameter | SQL Server | Oracle | OLE DB | ODBC |
| :--- | :--- | :--- | :--- | :--- |
| Data Provider | SqlClient | OracleClient | OleDb | Odbc |
| Namespace | System.Data.SqlClient | System.Data.OracleClient | System.Data.OleDb | System.Data.Odbc |
| Connection | SqlConnection | OracleConnection | OleDbConnection | OdbcConnection |
| Command | SqlCommand | OracleCommand | OleDbCommand | OdbcCommand |
| Data Adapter | SqlDataAdapter | OracleDataAdapter | OleDbDataAdapter | OdbcDataAdapter |
| Data Parameter | SqlParameter | OracleParameter |  |  |

