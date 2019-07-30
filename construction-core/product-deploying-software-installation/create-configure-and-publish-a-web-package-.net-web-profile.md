# Create, configure, and publish a web package \(.NET Web Profile\)

### App Configuration

App configuration in ASP.NET Core is based on key-value pairs established by configuration providers. Configuration providers read configuration data into key-value pairs from a variety of configuration sources:

* Azure Key Vault
*  Command-line arguments
*  Custom providers \(installed or created\)
* Directory files
*  Environment variables
*  In-memory .NET objects
* Settings files

```csharp
public Startup(IHostingEnvironment env)
{
    var builder = new ConfigurationBuilder()
        .SetBasePath(env.ContentRootPath)
        .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
        .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true)
        .AddEnvironmentVariables();
    Configuration = builder.Build();
}

public IConfigurationRoot Configuration { get; }

```

**Default configuration**

CreateDefaultBuilder provides default configuration for the app in the following order:

* Host configuration is provided from:
  * **Environment variables** prefixed with ASPNETCORE __\(for example, _ASPNETCORE\_ENVIRONMENT_\)
  * **Command-line arguments** using the Command-line Configuration Provider
* App configuration is provided from:
  * `appsettings.json` using the File Configuration Provider
  * `appsettings.{Environment}.json` using the File Configuration Provider
  * **SecretManager** when the app runs in the Development environment using the entry assembly
  * **Environment variables** using the Environment Variables Configuration Provider \(add custom prefix __with `.AddEnvironmentVariables(prefix: "PREFIX")`\)
  * **Command-line arguments** using the Command-line Configuration Provider

#### JSON example

Here is how `appsettings.json` looks like:

```text
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  }
}
```

{% hint style="info" %}
The setting keys are case **insensitive**.
{% endhint %}

#### **Custom configuration provider**

You can create your own configuration provider that, for example, reads configuration key-value pairs from a database using Entity Framework \(EF\) or from Consul.

### Security concerns

* Never store passwords or other sensitive data in configuration provider code or in plain text configuration files.
* Don't use production secrets in development or test environments.
* Specify secrets outside of the project so that they can't be accidentally committed to a source code repository.

### **.NET Core application deployment**

You can create three types of deployments for .NET Core applications:

* **Framework-dependent deployment \(FDD\)**. It relies on the presence of a shared system-wide version of .NET Core on the target system. FDDs contain _.dll files_ that can be launched by using the dotnet utility from the command line. For example, `dotnet app.dll` runs an application named app.
* **Framework-dependent executables \(FDE\).** Produces an _executable_ \(not _dll_\) that runs on a target platform. Similar to FDDs, framework-dependent executables  are platform-specific and aren't self-contained.
* **Self-contained deployment \(SCD\).** Unlike FDD/FDE, a SCD doesn't rely on the presence of shared components on the target system. All components, including both the .NET Core libraries and the .NET SCDs include an executable \(such as app.exe on Windows platforms\), and a .dll file \(such as app.dll\).

### Dotnet publish command

The  setting of the project file specifies the default target framework when you publish your app. You can change the target framework to any valid **Target Framework Moniker \(TFM\)**. For example, if your project uses _netcoreapp2.2_, a binary that targets .NET Core 2.2 is created. The TFM specified in this setting is the default target used by the _dotnet publish_ command.

You can publish one of the frameworks with the `dotnet publish -f` command. If you want to target more than one framework, you can set the  setting to more than one TFM value separated by a semicolon \(`netcoreapp2.1;netcoreapp2.2`\).

The default build configuration mode is **Debug** unless changed with the `-c` parameter.

You must \(except for .NET Core 3.x when you target the current platform\) use the following switches with the `dotnet publish` command to publish an FDE:

* `-r <RID>`. This switch uses an identifier \(RID\) to specify the target platform.
* `--self-contained false`. This switch tells the .NET Core SDK if it should be an FDE or SCD.

