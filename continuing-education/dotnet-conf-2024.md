# DotNET Conference 2024 Notes and Takeaways

Microsoft provides a yearly conference that highlights new technologies and capabilities with the DotNET.vNext.

## Key Note

Speakers:

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

Dot NET Release Notes:

- Modern Workloads, Developer Productivity, and Fundametals for building apps.
- .NET is a stack: Building blocks of rules and languages.
- Hightlight: .NET Aspire: Start, build, and deploy.

### Aspire

AppHost:

- Single entrypoint to a solution.
- All details of resources are injected at start-up time.

Dashboard:

- View of what's happening _right now_ with access to other Aspire features.
- Details including command-line args, env vars, etc.
- State information and Logs.
- Pin Icon: Persistent resource that stays online between Container and Project restarts.
- Open Telemetry: Structured logging integrated into entire application. Includes a trace view, enabling drill-down into operation details, and metrics on runtime health, etc.

Service Defaults:

- Obfuscates configuration and integrations.
- Intended to be modified on day one, or later in the project lifetime.
- Integrations are Hosting or Client type: Containers, Cloud Resources, EventBus.
- Pacakages bring-in Hosting Integrations.
- Use chained methods to add "Companion Services".

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

- Target Windows, Mac, IoS, and Linux devices.
- Hybrid web-view: Reuse components from any JavaScript framework.
- MAUI Embedding API's have been updated.
- Syncfusion Toolkit for .NET MAUI: Free, OSS controls for charts, carousel tab view, Shimmer (loading indicators), and more.
- 'main' Page is deprecated, instead `override Window CreateWindow()` method to build a new Window with a new AppShell.
- Integrate toolkits in 'MauiProgram.cs' entrypoint using AppBuilder.
- SQLite support.
- New CollectionView handler for iOS, MacCatalyst.

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

## References

## Footer

- Return to [Conted Index](./conted-index.html)
- Return to [README](../README.html)
