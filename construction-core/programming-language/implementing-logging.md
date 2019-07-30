# Implementing logging

{% hint style="success" %}
**Logging** \(sometimes also called tracing\) is used to record information about a program's execution for debugging and testing purposes.
{% endhint %}

Developers, testers and support engineers often use logging and tracing techniques to identify software problems, for post-deployment debugging, monitoring live systems and auditing purposes.

Logging usually involves writing text messages to log files or sending data to monitoring applications. Advanced and modern logging tools also support logging of complex data structures, call stacks, threading behavior and also support real-time monitoring of applications over a network or on a local machine.

## Serilog

Like many other libraries for .NET, Serilog provides diagnostic logging to files, the console, and elsewhere. It is easy to set up, has a clean API, and is portable between recent .NET platforms.

_Unlike_ other logging libraries, Serilog is built with powerful _structured event data_ in mind.

#### Text formatting

Serilog _message templates_ are a simple DSL extending .NET format strings. Parameters can be named, and their values are serialized as properties on the event for incredible searching and sorting flexibility:

```csharp
var position = new { Latitude = 25, Longitude = 134 };
var elapsedMs = 34;

Log.Information("Processed {@Position} in {Elapsed:000} ms.", position, elapsedMs);
```

This example records two properties, `Position` and `Elapsed` along with the log event. The properties captured in the example, in JSON format, would appear like:

```javascript
{"Position": {"Latitude": 25, "Longitude": 134}, "Elapsed": 34}
```

### Installation

Browse the Serilog tag on **NuGet** to see the available sinks, extensions and related third-party packages.

```text
PM> Install-Package Serilog
PM> Install-Package Serilog.Sinks.Console
```

### Configuration basics

#### Creating a logger

Loggers are created using a `LoggerConfiguration` object:

```csharp
Log.Logger = new LoggerConfiguration().CreateLogger();
Log.Information("No one listens to me!");
```

#### Sinks

This example will use the **console sink** package, which pretty-prints log data, and the **file sink** package, which writes log events to a set of date-stamped text files.

```text
Install-Package Serilog.Sinks.Console
Install-Package Serilog.Sinks.File
```

Sinks are configured using the `WriteTo` configuration object. Multiple sinks can be active at the same time. Adding additional sinks is a simple as chaining `WriteTo` blocks:

```csharp
Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("log-.txt", rollingInterval: RollingInterval.Day)
    .CreateLogger();
```

#### Minimum level

| Level | Usage |
| :--- | :--- |
| `Verbose` | Verbose is the noisiest level, rarely \(if ever\) enabled for a production app. |
| `Debug` | Debug is used for internal system events that are not necessarily observable from the outside, but useful when determining how something happened. |
| `Information` | Information events describe things happening in the system that correspond to its responsibilities and functions. Generally these are the observable actions the system can perform. |
| `Warning` | When service is degraded, endangered, or may be behaving outside of its expected parameters, Warning level events are used. |
| `Error` | When functionality is unavailable or expectations broken, an Error event is used. |
| `Fatal` | The most critical level, Fatal events demand immediate attention. |

### Writing Log Events

Log events are written to sinks using the `Log` static class, or the methods on an `ILogger`. These examples will use `Log` for syntactic brevity, but the same methods shown below are available also on the interface.

