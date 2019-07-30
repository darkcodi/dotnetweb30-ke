# Working with data providers

### Data providers

The following table lists the data providers that are included in the .NET Framework.

| .NET Framework data provider | Description |
| :--- | :--- |
| .NET Framework Data Provider for SQL Server | Provides data access for Microsoft SQL Server. Uses the `System.Data.SqlClient` namespace. |
| .NET Framework Data Provider for OLE DB | For data sources exposed by using OLE DB. Uses the `System.Data.OleDb` namespace. |
| .NET Framework Data Provider for ODBC | For data sources exposed by using ODBC. Uses the `System.Data.Odbc` namespace. |
| .NET Framework Data Provider for Oracle | For Oracle data sources. The .NET Framework Data Provider for Oracle supports Oracle client software version 8.1.7 and later, and uses the `System.Data.OracleClient` namespace. |
| EntityClient Provider | Provides data access for Entity Data Model \(EDM\) applications. Uses the `System.Data.EntityClient` namespace. |
| .NET Framework Data Provider for SQL Server Compact 4.0. | Provides data access for Microsoft SQL Server Compact 4.0. Uses the `System.Data.SqlServerCe` namespace. |

### Core Objects of Data Providers <a id="core-objects-of-net-framework-data-providers"></a>

The following table outlines the four core objects that make up a .NET Framework data provider.

| Object | Description |
| :--- | :--- |
| `Connection` | Establishes a connection to a specific data source. The base class for all `Connection`objects is the `DbConnection` class. |
| `Command` | Executes a command against a data source. Exposes `Parameters` and can execute in the scope of a `Transaction` from a `Connection`. The base class for all `Command` objects is the `DbCommand` class. |
| `DataReader` | Reads a forward-only, read-only stream of data from a data source. The base class for all `DataReader` objects is the `DbDataReader` class. |
| `DataAdapter` | Populates a `DataSet` and resolves updates with the data source. The base class for all `DataAdapter` objects is the `DbDataAdapter` class. |

