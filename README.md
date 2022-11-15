**What is Serilog?**

Serilog is a logging library for .NET and C# that allows for more detailed and structured logging than the default .NET logging library. Serilog can be used to log information about application events, errors, and performance metrics. This information can be used to troubleshoot issues with an application or to monitor its performance over time.

**What is Structured Logging?**

Structured logging allows you to store your log data in a format that is easy to process and search. It also allows you to add custom fields to your logs, which can be used to track specific information about your application. It is a method of logging that uses a predefined format to store log data. This makes it easier for developers and programmers to parse and analyze log data.

**What are Serilog Sinks?**

Sinks in Serilog are the log targets (i.e., they are the destinations where you would like to send your logs). Some of the popular sinks are file and console targets. Anything that can store log data can be used as a Serilog sink. Serilog comes with a number of built-in sinks, but you can also create your own custom sinks.

**Note:** serilog support lots of sinks in-built like:

<img width="606" alt="serilog-architecture" src="https://user-images.githubusercontent.com/85872541/201994086-a0e67428-9aee-4a2e-a57d-6720d3afb637.png">

**Log Event Levels**

Serilog uses levels as the primary means for assigning importance to log events. The levels in increasing order of importance are:


![image](https://user-images.githubusercontent.com/85872541/201994511-2f5efc3b-8f5f-4067-b4fa-16a70e2556aa.png)


**Enrichers**

Enrichers are simple components that add, remove or modify the properties attached to a log event. This can be used for the purpose of attaching a thread id to each event, for example:

```ruby
Log.Logger = new LoggerConfiguration()
    .Enrich.With(new ThreadIdEnricher())
    .WriteTo.Console(
        outputTemplate: "{Timestamp:HH:mm} [{Level}] ({ThreadId}) {Message}{NewLine}{Exception}")
    .CreateLogger();

````

**Customizing the stored data**

To customise how Serilog persists a destructured complex type, use the Destructure configuration object on LoggerConfiguration:

```ruby
Log.Logger = new LoggerConfiguration()
    .Destructure.ByTransforming<HttpRequest>(
        r => new { RawUrl = r.RawUrl, Method = r.Method })
    .WriteTo...
```
This example transforms objects of type HttpRequest to preserve only the RawUrl and Method properties. A number of different strategies for destructuring are available, and custom ones can be created by implementing IDestructuringPolicy.
