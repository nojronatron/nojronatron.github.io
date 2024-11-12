# DotNET Conference 2024 Notes and Takeaways

Microsoft provides a yearly conference that highlights new technologies and capabilities with the DotNET.vNext.

## Key Note

Speakers and Presenters:

- James Montemagno
- Maddy
- Damian Edwards
- Pedram R
- Maria N
- Steve S
- David O
- Mark B (Fidelity ActiveTrade and .NET 9 announcement)
- Safia A
- Daniel R
- Filisha S
- Rachel K

Dot NET Release Notes:

- Modern Workloads, Developer Productivity, and Fundametals for building apps.
- .NET is a stack: Building blocks of rules and languages.
- Hightlight: .NET Aspire: Start, build, and deploy.

### Aspire

Is Open Source!

AppHost:

- Single entrypoint to a solution.
- All details of resources are injected at start-up time.

Dashboard:

- View of what's happening _right now_ with access to other Aspire features.
- Details including command-line args, env vars, etc.
- State information and Logs.
- Pin Icon: Persistent resource that stays online between Container and Project restarts.
- Open Telemetry: Structured logging integrated into entire application. Includes a trace view, enabling drill-down into operation details, and metrics on runtime health, etc.
- All data is stored in memory for local/debug, but for Deployment it can be configured to store in OpenTelemetry data to wherever is set up to receive it.
- .NET Aspire Dashboard is "more than a viewer": Can use the `Actions` column icons to start, stop, and restart a Project.

Service Defaults:

- Obfuscates configuration and integrations.
- Intended to be modified on day one, or later in the project lifetime.
- Integrations are Hosting or Client type: Containers, Cloud Resources, EventBus.
- Pacakages bring-in Hosting Integrations.
- Use chained methods to add "Companion Services".
- Integrations defined: Components that are added and configured Within App Host file. Client Integrations is similar, but supporting client-side components like Redis, etc.

Announced: [.NET Aspire Community Toolkit](github.com/CommunityToolkit/aspire)

Xbox Live:

- Now using .NET Aspire.
- Tightened-up development loop.

Copilot:

- Leverages .NET Aspire.
- Increased application speed and efficiencies including development cycle.
- Measurably increased Uptime.

MSLearn:

- .NET Aspire training modules now available.

Azure Functions:

- Integrations now available!
- Currently in Preview.

Container Support:

- Docker.
- PodMan.
- _Lack_ of a Containerization system without ucrashing.

### .NET and AI

Learn, integrate, collaborate, deploy:

- .NET is at core of Microsoft and GitHub Copilot.
- IChatClient: Interface represents any AI Chat Model.
- Semantic Search.
- Natural Language interpretation including multi-lingual capabilities.
- Dependency Injection is used to swap-in/out between Chat Clients.
- 'pipeline': ChatClient capability enables configuring Chat Options or other 'PipelineStep' items.

Pieces for Developers:

- VSCode and Teams plugin extensions.

### .NET MAUI

New Stuff in MAUI:

- Target Windows, Mac, IoS, and Linux devices.
- Hybrid web-view: Reuse components from any JavaScript framework.
- MAUI Embedding API's have been updated.
- Syncfusion Toolkit for .NET MAUI: Free, OSS controls for charts, carousel tab view, Shimmer (loading indicators), and more.
- 'main' Page is deprecated, instead `override Window CreateWindow()` method to build a new Window with a new AppShell.
- Integrate toolkits in 'MauiProgram.cs' entrypoint using AppBuilder.
- SQLite support.
- New CollectionView handler for iOS, MacCatalyst.

More:

- WinUI, Mac Catalyst, iOS, and Android still supported!
- Blazor Hybrid or WinUI only, still supported.
- Lots of growth of usage and community involvement throughout 2024.
- Many partners and implementers diving-in, with over 2.6x growth in Google Play Store apps using .NET MAUI.
- OSS Charts and Controls using [Syncfusion Controls for MAUI](https://github.com/syncfusion/maui-toolkit).
- MAUI Setup template includes "Include Sample Content" checkbox that will put MVVM folder structure and files to help get started, including .NET MAUI and Syncfusion Toolkits.
  - Shell Routing and DI already configured!
  - Toasts and Charts!
  - Pre-styled controls, floating text labels, etc.
- Release schedule:
  - 18-month cycles that overlap with .NET releases.
  - Dependent on Xcode and Android release cycles.
  - Xamarin support ended and will no longer be included.
- XAML Live Preview _outside of debug mode_.
-

### ASP.NET Core

- Performance, accessibity, and security updates.
- Built-in OpenAPI support, Blazor enhancements, and improved tooling and debugging.
- AOT support, and improvmeents to monitoring and tracing.
- WebSocket message compression for Blazor Server.
- Precommpression and improved cashing for static web assets.
- `MapStaticAssets()` replaces `UseStaticFiles()` middleware. Use `@Assets` API to use optimized verisons.
- `@rendermode InteractiveServer` sets up websocket between server and client to support things like in-app Chat.
- `RenderInfo` API: Enabled boolean decisions to placeholder while loading data, disabling buttons until data loaded, etc.
- OpenAPI integration into Blazor back-end: `app.MapOpenApi()` expose OpenAPI tooling. JSON configuration page is generated when configured in DI.

### GitHub Copilot

- More contextual awareness.
- Visual Studio integration improvements: GH Copilot Chat included by default.
- Copilot Edits: Multi-file edits!

### What's New In C# 13

- Get an overview of language features at Learn.Microsoft.com
  - Includes Preview features.
- Look at 'roslyn' GitHub project docs folder to see what is going on with current rev of C#.

## ASP.NET Core and Blazor

ASP.NET Core:

- Full stack web framework.
- Tooling.
- Quality and Fundamentals.
- Performance, accessibility, and security.
- Developer experience: Open APIs, and tooling and debuging improvements.
- Cloud Native: AOT and improved monitoring and tracing.
- Adaptive Garbage Collection with .NET 9.
- Simple to integrate .NET Aspire into .NET Core App!
- .NET Aspire integration makes dev and debugging simpler than without - just use the Aspire Dashboard.
- Publishing via Visual Studio: Understands .NET Aspire integration with Blazor, use as before to push to production and/or cloud.

New Blazor Features in .NET 9:

- Detect component render mode _at runtime_.
- Improve reconnetion logic.
- Static SSR in globally interactive app.
- Simplified authentication state serialization.
- Component constructor injection.
- Blazor Hybrid + Web Project Template now included!

Render Mode Setting and Detection:

- In Component declarations use `@rendermode InteractiveAuto`.
- Use `@RendererInfo` to get render mode information using its props like `Name` or `IsInteractive`.
- Placeholder static HTML is sent to client before WASM (or Server) rendering completes, then page is swapped out (lifecycle improvements).

Reconnection Experience with Interactive Server Rendering:

- Prior to .NET 9: Default UX tells user the server is trying to reconnect.
- .NET 9 now: Better UX during reconnect including stand-in page.

Blazor Hybrid:

- Run Blazor components natively in client app and render through a WebApp control.
- Target web, desktop, and mobile _all in one app_. :tada:
- Was available in .NET 8, now in .NET 9 this is simplified! :astonished:

Static Web Assets:

- All static web assets collected during build-run and use compression.
- Fingerprint all files with hashes upon publish. Includes CSS files.
- Static assets now presented as _endpoints_ so auth policies (etc) can be _added to static files_. :astonished:
- Use `app.MapStaticAssets()` API to present static assets as endpoings (with optimizations).
- Use `@Assets[]` to map static assets to optimized, precompressed versions.
- Use `<ImportMap />` to automate mapping JS files for import.
- Immutable Caching to tell the browser to maintain CSS or other static files that will actually _never change_, improving WRRC time.

Built-in OpenAPI Support:

- Both Minimal APIs and Controller-based APIs!
- Can customize document generation via transformers.
- Use existing UIs and libraries.
- An updated Microsoft.OpenAI package must be NuGet imported.
  - Swagger w/ Swashbuckle APIs can be added!
  - Add it to the DI Container where 'Configure HTTP request pipeline' is e.g. next to `app.MapOpenApi()`.
- Includes integration to AOT compilation.

SignalR Improvements:

- Native AOT Supprot.
- Polymorphic type support.
- Improved Activity Tracing (split-out to separate threads instead of SignalR as a whole).
- Problems with `IDistributedCache` replaced by using `HybridCache` type instead!
  - Serialization, stampeded protection, L1/L2 support, low-allocation API, tagging and invalidation, back-support to .NET 8!
  - Single API call and pass in the string and ID, as well as a CencellationToken and it will do the rest.
  - Currently Preview, will release with future .NET 9 improvement.

Other:

- Ability to trust ASP.NET Core Dev Cert on Linux.
- Endpoint metadata added to Dev Exceptions Page.
- Improved blazor WASM and disctionary debugging.
- WASM Live Debug!
  - No longer displays JavaScript primitives, uses .NET Primitives instead.
  - Immediate Window works!
  - Currently in Preview for early .NET 9 release.
- Dictionary View of HTTP Headers in debugger.

## References

- [.NET Aspire Samples](https://github.com/dotnet/aspire-samples)
- [.NET Aspire Community Toolkit](https://github.com/CommounityToolkit/Aspire)
- [Get Started with .NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire/)
- [.NET Aspire on GitHub](https://github.com/dotnet/aspire)
- [.NET Aspire Training on MSLearn](https://learn.microsoft.com/en-us/training/modules/introduction-dotnet-aspire/)
- [Use IChatClient and IEmbeddingGenerator to access AI Services](https://aka.ms/m.e.ai)
- [Fluent UI Blazor components](aka.ms/blazor/fluentui)
- [.NET Aspire Credential Assessment Informaiton](https://learn.microsoft.com/en-us/credentials/applied-skills/build-distributed-apps-with-dotnet-aspire/)

## Footer

- Return to [Conted Index](./conted-index.html)
- Return to [README](../README.html)
