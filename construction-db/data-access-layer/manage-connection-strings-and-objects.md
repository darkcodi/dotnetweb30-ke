# Manage connection strings and objects

Storing the connection string in a configuration file gives you much more flexibility because you can simply edit the file and change the settings if you change or add a server.

{% hint style="danger" %}
Connection strings \(and all other sensitive information\) should be **encrypted** or **hashed** wherever possible. Storing a database connection string in plain-text \(human readable\) form can present a huge security vulnerability and should be avoided if possible.
{% endhint %}

By default, you can access the ConnectionStrings property almost identically to how you access AppSettings.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
   <connectionStrings>
      <clear />
      <add name="AdventureWorksString" providerName="System.Data.SqlClient" connectionString="Data Source=localhost;Initial Catalog=AdventureWorks;Integrated Security=true" />
      <add name="MarsEnabledSqlServer2005String" providerName="System.Data.SqlClient" connectionString="Server=Aron1;Database=pubs;Trusted_Connection=True;MultipleActiveResultSets=true" />
      <add name="OdbcConnectionString" providerName="System.Data.Odbc" connectionString="Driver={Microsoft Access Driver (*.mdb)};Dbq=C:\adatabase.mdb; Uid=Admin;Pwd=R3m3emberToUseStrongPasswords;" />
      <add name="AccessConnectionString" providerName="System.Data.OleDb" connectionString="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=\PathOrShare\mydb.mdb;User Id=admin;Password=Rememb3rStr0ngP4sswords;" />
      <add name="OracleConnectionString" providerName="System.Data.OracleClient" connectionString="DataSource=MyOracleDB;Integrated Security=yes;" />
   </connectionStrings>
</configuration>
```

