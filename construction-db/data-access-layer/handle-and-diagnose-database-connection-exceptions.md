# Handle and diagnose database connection exceptions

When opening a connection to the database server, an exception might be thrown because the server is not available. The connection timeout defaults to 15 seconds, and you should consider your scenario to decide whether to increase or decrease this time. For fast networks, you might lower this time so you can fail quickly.

Why wait more than five seconds to fail when you know that most of your connections take only one second? However, if you’re on a slow connection, you might set the connection timeout to a higher value.

Example:

```text
"server=.;database=northwind;integrated security=true;connection timeout=30"
```

There are many scenarios in which you can’t prevent an exception proactively. For example, the server loses power. This is when you can benefit from the try/catch block in your code. If an exception is thrown, you should have catch blocks for each type of exception for which you have specific handling.

```csharp
try
{
    var cnSetting = ConfigurationManager.ConnectionStrings["nw"];
    using (var cn = new SqlConnection())
    using (var cmd = cn.CreateCommand())
    {
        cn.ConnectionString = cnSetting.ConnectionString;
        cmd.CommandTimeout = 60;
        cmd.CommandText = "Select @@version";
        cn.Open();
        MessageBox.Show(cmd.ExecuteScalar().ToString());
    }
}
catch (SqlException ex)
{
    MessageBox.Show("SQL Exception: " + ex.Message);
}
```

For connection timeout, `SqlException` will have `-2` in `Number` property.

