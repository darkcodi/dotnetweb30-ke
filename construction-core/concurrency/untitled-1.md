# How to run Background Tasks in ASP.NET

[WEBBACKGROUNDER](https://github.com/NuGet/WebBackgrounder?WT.mc_id=-blog-scottha)

[WebBackgrounder](https://github.com/NuGet/WebBackgrounder?WT.mc_id=-blog-scottha) is a proof-of-concept of a web-farm friendly background task manager meant to just work with a vanilla ASP.NET web application.

The goal of this project is to handle one task only, manage a recurring task on an interval in the background for a web app.

If your ASP.NET application just needs one background task to runs an a basic scheduled interval, than perhaps you just need the basics of WebBackgrounder.

Somewhat in response to the need for WebBackgrounder, [.NET 4.5.2 added QueueBackgroundWorkItem as a new API](http://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx?WT.mc_id=-blog-scottha). It's described in above section.

[FLUENTSCHEDULER](https://github.com/jgeurts/FluentScheduler?WT.mc_id=-blog-scottha)

FluentScheduler is a more sophisticated and complex scheduler that features a fluent interface. You have really explicit control over when your tasks run.

FluentScheduler also embraces IoC and can easily plug into Dependency Injection tool of choice by just implementing their ITaskFactory interface.

[QUARTZ.NET](http://www.quartz-scheduler.net/)

Quartz.NET is a .NET port of the popular Java job scheduling framework of the \(almost\) same name. It's very actively developed. Quartz has an IJob interface with just one method, Execute, to implement.

[HANGFIRE](http://hangfire.io/)

The most polished of the group, [Hangfire](http://hangfire.io/). It's even optionally backed by Redis, SQL Server, SQL Azure, MSMQ, or RabbitMQ for reliability.

The best feature from Hangfire is its built in /hangfire dashboard that shows you all your scheduled, processing, succeeded and failed jobs.

