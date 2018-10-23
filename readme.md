# About

This repository is for Sentry bug report.

It have expected that the `IWebHostBuilder.UseSentry()` extension method would fail silently if there is no "Sentry" settings node present. It also appeared so, until I have noticed below exception on **shutting down** the console host:


```
Unhandled Exception: System.NullReferenceException: Object reference not set to an instance of an object.
   at Sentry.Internal.OptionalHub.Dispose() in C:\projects\sentry-dotnet\src\Sentry\Internal\OptionalHub.cs:line 53
   at Microsoft.Extensions.DependencyInjection.ServiceLookup.ServiceProviderEngineScope.Dispose()
   at Microsoft.Extensions.DependencyInjection.ServiceLookup.ServiceProviderEngine.Dispose()
   at Microsoft.Extensions.DependencyInjection.ServiceProvider.Dispose()
   at Microsoft.AspNetCore.Hosting.Internal.WebHost.Dispose()
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.RunAsync(IWebHost host, CancellationToken token, String shutdownMessage)
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.RunAsync(IWebHost host, CancellationToken token)
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.Run(IWebHost host)
   at SentryNoSilentFail.Program.Main(String[] args) in C:\dev\playground\SentryNoSilentFail\SentryNoSilentFail\Program.cs:line 21
2018-10-23 18:43:15.9882||1|FATAL|SentryNoSilentFail.Program|Program stopped because of exception. System.NullReferenceException: Object reference not set to an instance of an object.
   at Sentry.Internal.OptionalHub.Dispose() in C:\projects\sentry-dotnet\src\Sentry\Internal\OptionalHub.cs:line 53
   at Microsoft.Extensions.DependencyInjection.ServiceLookup.ServiceProviderEngineScope.Dispose()
   at Microsoft.Extensions.DependencyInjection.ServiceLookup.ServiceProviderEngine.Dispose()
   at Microsoft.Extensions.DependencyInjection.ServiceProvider.Dispose()
   at Microsoft.AspNetCore.Hosting.Internal.WebHost.Dispose()
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.RunAsync(IWebHost host, CancellationToken token, String shutdownMessage)
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.RunAsync(IWebHost host, CancellationToken token)
   at Microsoft.AspNetCore.Hosting.WebHostExtensions.Run(IWebHost host)
   at SentryNoSilentFail.Program.Main(String[] args) in C:\dev\playground\SentryNoSilentFail\SentryNoSilentFail\Program.cs:line 21
```

# How to reproduce
* Clone the repository
* In SentryNoSilentFail folder `dotnet run` or run the project in VS with "first chance" CLR Exceptions enabled
* You should get the above exception