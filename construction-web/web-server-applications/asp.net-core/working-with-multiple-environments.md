# Working with Multiple Environments

ASP.NET Core configures app behavior based on the runtime environment using an environment variable **`ASPNETCORE_ENVIRONMENT`**.

### ASPNETCORE\_ENVIRONMENT

ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at app startup and stores the value in `IHostingEnvironment.EnvironmentName`. You can set `ASPNETCORE_ENVIRONMENT` to any value, but three values are supported by the framework: **Development**, **Staging**, and **Production**. If `ASPNETCORE_ENVIRONMENT` isn't set, it defaults to `Production`.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    if (env.IsProduction() || env.IsStaging() || env.IsEnvironment("Staging_2"))
    {
        app.UseExceptionHandler("/Error");
    }

    app.UseStaticFiles();
    app.UseMvc();
}
```

{% hint style="warning" %}
On Windows and macOS, environment variables and values aren't case sensitive. Linux environment variables and values are **case sensitive** by default.
{% endhint %}

### launchSettings.json

The environment for local machine development can be set in the _Properties\launchSettings.json_ file of the project.

```javascript
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:54339/",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      }
    },
    "EnvironmentsSample": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:54340/"
    },
    "Kestrel Staging": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:51997/"
    }
  }
}
```

