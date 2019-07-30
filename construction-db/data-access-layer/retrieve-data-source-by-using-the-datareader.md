# Retrieve data source by using the DataReader

{% hint style="success" %}
A **DbDataReader** is a forward-only, read-only, server-side cursor, which provides a high-performance method of retrieving data from the data store.
{% endhint %}

The `DbDataReader` object contains a `Read` method that retrieves data into its buffer. **Only one row** of data is ever available at a time, which means that all the data from the database does not need to be completely read into the application before it is processed.

You can use `Read` method to get selection results and **continuously loop through the results** until the end of data has been reached \(when the `Read` method returns false\).

#### Example with `while` loop

```csharp
var nw = ConfigurationManager.ConnectionStrings["nw"];
var connection = new SqlConnection();
connection.ConnectionString = nw.ConnectionString;
var cmd = connection.CreateCommand();
cmd.CommandType = CommandType.Text;
cmd.CommandText = "SELECT ProductID, UnitPrice FROM Products";
connection.Open();
DbDataReader rdr = cmd.ExecuteReader();
while (rdr.Read())
{
    MessageBox.Show(rdr["ProductID"] + ": " + rdr["UnitPrice"]);
}
connection.Close();
```

#### Example with `DataTable`

```csharp
var nw = ConfigurationManager.ConnectionStrings["nw"];
var connection = new SqlConnection();
connection.ConnectionString = nw.ConnectionString;
var cmd = connection.CreateCommand();
cmd.CommandType = CommandType.Text;
cmd.CommandText = "SELECT ProductID, ProductName FROM Products";
connection.Open();
var rdr = cmd.ExecuteReader();
var products = new DataTable();
products.Load(rdr, LoadOption.Upsert);
connection.Close();
cmbProducts.DataSource = products;
cmbProducts.DisplayMember = "ProductName";
cmbProducts.ValueMember = "ProductID";
```

