# Troubleshoot ASP.NET Core projects

### .NET Core SDK warnings <a id="net-core-sdk-warnings"></a>

#### Both the 32-bit and 64-bit versions of the .NET Core SDK are installed <a id="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a>

Uninstall the 32-bit .NET Core SDK to prevent this warning. Uninstall from **Control Panel** &gt; **Programs and Features** &gt; **Uninstall or change a program**. If you understand why the warning occurs and its implications, you can ignore the warning.

#### The .NET Core SDK is installed in multiple locations <a id="the-net-core-sdk-is-installed-in-multiple-locations"></a>

You see this message when you have at least one installation of the .NET Core SDK in a directory outside of _C:\Program Files\dotnet\sdk\_. Usually this happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.

#### No .NET Core SDKs were detected <a id="no-net-core-sdks-were-detected"></a>

* Install the .NET Core SDK. Obtain the latest installer
* Verify that the `PATH` environment variable points to the location where the SDK is installed

### Obtain data from an app <a id="obtain-data-from-an-app"></a>

If an app is capable of responding to requests, you can obtain the following data from the app using middleware:

* Request – Method, scheme, host, pathbase, path, query string, headers
* Connection – Remote IP address, remote port, local IP address, local port, client certificate
* Identity – Name, display name
* Configuration settings
* Environment variables

Place the **logging middleware** code at the beginning of the `Startup.Configure` method's request processing pipeline.

