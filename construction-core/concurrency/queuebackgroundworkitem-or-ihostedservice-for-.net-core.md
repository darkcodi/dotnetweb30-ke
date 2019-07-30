# QueueBackgroundWorkItem or IHostedService for .NET Core

How to reliably run a resource-intensive process  \(sending email, image processing, generating a PDF file\) on a background thread?

**QueueBackgroundWorkItem** \(QBWI\). This was specifically added to enable ASP.NET apps to reliably run short-lived background tasks.

QBWI schedules a task which can run in the background, independent of any request. This differs from a normal ThreadPool work item in that ASP.NET automatically keeps track of how many work items registered through this API are currently running, and the ASP.NET runtime will try to delay AppDomain shutdown until these work items have finished executing.

**IHostedService for .NET Core**  
 Since .NET Core 2.0, the framework provides a new interface named IHostedService helping you to easily implement hosted services. The basic idea is that you can register multiple background tasks \(hosted services\), that run in the background while your web host or host is running.

SignalR is one example of an artifact using hosted services, but you can also use it for much simpler things like:

·         A background task polling a database looking for changes

·         A scheduled task updating some cache periodically.

·         An implementation of QueueBackgroundWorkItem.

·         Processing messages from a message queue in the background of a web app while sharing common services such as ILogger.

When you register an IHostedService, .NET Core will call the **StartAsync\(\)** and **StopAsync\(\)** methods of your IHostedService type during application start and stop respectively. Specifically, start is called after the server has started and IApplicationLifetime.ApplicationStarted is triggered.

You could go ahead and create you custom hosted service class from scratch and implement the IHostedService, as you need to do when using .NET Core 2.0.

![](../../.gitbook/assets/image%20%2839%29.png)

