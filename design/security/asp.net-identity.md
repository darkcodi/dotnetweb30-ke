# ASP.NET Identity

### \[Obsolete\] Background: Membership in ASP.NET <a id="background-membership-in-aspnet"></a>

* **ASP.NET Membership** \(2005, Forms Authentication + SQL Server database to store user data\)
* **ASP.NET Simple Membership** \(2010, easier to add and more customazible regarding user info\)
* **ASP.NET Universal Providers** \(special for Microsoft Azure SQL Database or SQL Server Compact, with EF code first\)

### ASP.NET Identity <a id="aspnet-identity"></a>

Considering these changes in web application development, ASP.NET Identity was developed with the following goals:

* **One ASP.NET Identity system** for all ASP.NET frameworks, such as ASP.NET MVC, Web Forms, Web Pages, Web API.
* **Ease of plugging in profile data about the user**, eg you can easily enable the system to store birth dates.
* **Persistence control.** It's easy to plug in different storage mechanisms such as SharePoint, Azure Storage Table Service, NoSQL databases, etc.
* **Unit testability.** ASP.NET Identity makes the web application more unit testable.
* **Role provider** which lets you restrict access to parts of your application by roles.
* **Claims Based.** ASP.NET Identity supports claims-based authentication, where the user's identity is represented as a set of claims.
* **Social Login Providers.** You can easily add social log-ins such as Microsoft Account, Facebook, Twitter, Google, and others.
* **OWIN Integration.** ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.
* **NuGet package.** ASP.NET Identity is redistributed as a NuGet package.

