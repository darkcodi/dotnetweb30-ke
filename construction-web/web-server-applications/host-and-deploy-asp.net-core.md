# Host and deploy ASP.NET Core

In general, to deploy an ASP.NET Core app to a hosting environment:

* Deploy the published app to a folder on the hosting server.
* Set up a process manager that starts the app when requests arrive and restarts the app after it crashes or the server reboots.
* For configuration of a reverse proxy, set up a reverse proxy to forward requests to the app.

### Publish to a folder <a id="publish-to-a-folder"></a>

The `dotnet publish` command compiles app code and copies the files required to run the app into a _publish_ folder. The _publish_ folder contains one or more app assembly files, dependencies, and optionally the .NET runtime. A .NET Core app can be published as _self-contained deployment_ or _framework-dependent deployment_.

### Set up a process manager <a id="set-up-a-process-manager"></a>

An ASP.NET Core app is a console app that must be started when a server boots and restarted if it crashes. To automate starts and restarts, a process manager is required. The most common process managers for ASP.NET Core are:

* Linux
  * Nginx
  * Apache
* Windows
  * IIS
  * Windows Service

### Set up a reverse proxy <a id="set-up-a-reverse-proxy"></a>

If the app uses the Kestrel server, **Nginx**, **Apache**, or **IIS** can be used as a reverse proxy server. A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel.

