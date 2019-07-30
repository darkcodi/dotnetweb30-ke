# Updating data

### Update with `DbCommand`:

```csharp
var connection = new SqlConnection();
connection.ConnectionString = nw.ConnectionString;
var cmd = connection.CreateCommand();
cmd.CommandType = CommandType.StoredProcedure;
cmd.CommandText = "CustOrderHist";
DbParameter parm = cmd.CreateParameter();
parm.ParameterName = "@Id";
parm.Value = "ANATR";
cmd.Parameters.Add(parm);
```

### Update with `DbDataAdapter`:

```csharp
var nw = ConfigurationManager.ConnectionStrings["nw"];
var connection = new SqlConnection();
connection.ConnectionString = nw.ConnectionString;
var cmd = connection.CreateCommand();
cmd.CommandType = CommandType.Text;
cmd.CommandText = "SELECT * FROM Customers";
var da = new SqlDataAdapter(cmd);
var nwSet = new DataSet("nw");
var bldr = new SqlCommandBuilder(da);
da.Fill(nwSet, "Customers");

//Modify existing row
var customersTable = nwSet.Tables["Customers"];
var updRow = customersTable.Select("CustomerID='WOLZA'")[0];
updRow["CompanyName"] = "New Wolza Company";

//Add new row
customersTable.Rows.Add(
"AAAAA", "Five A Company");

//Delete a row, note that you cannot delete a
//customer who has orders
var delRow = customersTable.Select("CustomerID='PARIS'")[0];
delRow.Delete();

//send changes to database
da.Update(nwSet, "Customers");
dataGridView2.DataSource = nwSet;
dataGridView2.DataMember = "Customers";
MessageBox.Show("Update Complete");
```

