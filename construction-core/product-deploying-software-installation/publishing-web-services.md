# Publishing Web Services

### **Publish to a folder**

The `dotnet publish` command compiles app code and copies the files required to run the app into a publish folder. When deploying from Visual Studio, the `dotnet publish` step occurs automatically before the files are copied to the deployment destination.

#### **Folder contents**

The publish folder contains:

* one or more app assembly files,
* dependencies,
* \(optionally\) the .NET runtime.

### Set up a process manager

An ASP.NET Core app is a console app that must be started when a server boots and restarted if it crashes. To automate starts and restarts, a process manager is required. 

The most common process managers for ASP.NET Core are:

* Linux
  * Nginx
  * Apache
* Windows
  * IIS
  * Windows Service

### **Set up a reverse proxy**

If the app uses the Kestrel server, Nginx, Apache, or IIS can be used as a reverse proxy server.

A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel. Either configuration—with or without a reverse proxy server—is a supported hosting configuration.

### **Proxy server and load balancer scenarios**

Additional configuration might be required for apps hosted behind proxy servers and load balancers. Without additional configuration, an app might not have access to the scheme \(HTTP/HTTPS\) and the remote IP address where a request originated.

