# DotNET Conference 2024 Notes and Takeaways

Microsoft provides a yearly conference that highlights new technologies and capabilities with the DotNET.vNext.

## Table of Contents

- [Key Note](#key-note)
- [ASP.NET Core and Blazor](#aspnet-core-and-blazor)
- [Hybrid Cache](#hybrid-cache)
- [A Selection Of Recent C# Language Features](#a-selection-of-recent-c-language-features)
- [OpenAI DotNET The Official OpenAI Library for .NET](#openai-dotnet-the-official-openai-library-for-net)
- [References](#references)
- [Footer](#footer)

## Key Note

Speakers and Presenters (throughout the event):

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
- David Fowler
- Mark Gravell
- Bill Wagner
- Scott Addie
- Luis Quintanilla
- Tanner Gooding
- Tarek Sayed
- Jordan Matthiesen
- Brain Randell (GitHub) (octobrian)

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

## Hybrid Cache

- Works in ASP.NET
- _Also works in your other .NET Apps_!
- Helps to reduce Stampedes: A busy site where cache expires and suddenly all clients receiving a cache-miss, followed by the expensive operation, with massing cache updating.
- Releasing _alongside .NET 9_, therefore _available for both 8 and 9_.
- Helps avoid cache breaking under certain pressure scenarios.
- Is observable, with events and counters.
- Tag support: bulk invalidation by category.
- Has a default implementation and is an abstraction (for custom implementation?).
- Expiration can be set globally or per-call.
- Mutable and Immutable types are supported.

Demo:

- An app without cache: Whenever an 'expensive resource' is used, consider adding cache between the front-end and back-end.
  - GUIDs change with every page reload (Blazor).
- `IMemoryCache`: Uses a unique, parameterized key, then use the Get-Set of the MemoryCache API to decide whether to do 'expensive' operation or return existing Value(s).
  - GUIDs no longer change unless the cache has expired.
  - Running in-process memory, won't withstand cold-start.
  - No serialization of the cached object.
  - Mutable objects could be changed unexpectedly, and is therefore a security and performance threat.
- `IDistributedCache`: Similar to IMemoryCache but includes active-process stores.
  - File system, SQLite, Redis, etc...any storage outside of the process.
  - More code required to leverage.
  - Serialization is required (JSON, XML, etc) to update the cache.
  - Deserialization happens every time a cache hit happens.
  - Relying on Redis, etc, implies latency of that service and/or failover or unavailable instance risks.
- `HybridCache`: Attempts to bridge the features of the above
  - Requires a new package refernece to the Project configuration.
  - Register as a DI Container Service (via App.builder()).
    - Configure expiration, etc here.
  - Less code necessary to implement at the controller (or minimal API endpoint).
  - Get or Create is an Async call: `GetOrCreateAsync()`
  - The same data is stored on a per-page-basis, instead of per session.
  - In-process and out-of-process memories are utilized under the hood by Hybrid Cache.
  - Stampeding: Requests wanting the same expired data, only one process updates the cache on a cache miss, then subsequent queued requests get the cached result.
  - Leverages JSON Serialization by default, other serializers and configurations are available.
  - The key is in the `GetOrCreateAsync()` method.
  - State can be passed-in using additional API calls.

## A Selection Of Recent C# Language Features

Pattern Matching:

- Declaritively write what historically has been done using If-then-else and select-case statements.
- Historically, it can be frustrating to ensure all possible code paths result in outputs.
  - Pattern Matching ensures the compiler flags these situations so they get fixed before build or run.
- Use a discard pattern (using the Discard operator) to handle 'all other cases' in a switch-case block.
- Statements like `num is not 4 or 9` is a non-obvious bug if the intent is for _neither_ 4 _nor_ 9 to be matched.
  - Rewrite it to `num is not (4 or 9)` as a compound pattern.
  - Future compiler release will detect this and warn accordingly.

File Scoped Namespaces:

- Instead of `namespace NamespaceName { ... }` use `namespace NamespaceName;`
  - Saves space.
  - Will add "whitespace diff" in git, but that can be configured to reduce whitespace diff to a change in braces to a single semicolon.

Class Properties with init and required:

- Public nullable properties if not set with a CTOR or with an assignment.
- `required` keyword: If a new object is instantiated but not assigned, the calling code will show the 'required' warning.
  - Blocks caller initialization of required property outside of a CTOR.
- `init`: Use in space of `set` to allow setting the property _once_, similar to read-only.
  - This is a way to show _intent_ of the property data.

Strings!

- As JSON (in particular) and string are used more commonly for passing data back and forth:
  - There are code security risks.
  - Quoted literals: `"my string value"`
- Raw String Literal: Use three or more double-quotation marks to enclose a string, to maintain formatting during initialization, but ignoring whitespace during processing.
- Interpolated strings:
  - `$"Hello {value}"`
  - `@"Hello """{name}""""`
  - JSON interpolation adds additional braces `{{}}` to set up the interpolated expression.
    - Since JSON uses curly braces to start with, doubling-up is interpreted as a JSON Interpolation String.
- THere were other examples (but I messed them).

Records:

- Added keyword to a `Class` declaration.
- `record` generates lots of code for you.
- Says: Primary purpose is to hold data (state).
- Also indicates: NOT a functional entity or object!
- Enables use of `with` keyword.
  - A `struct` also enables use of `with`.
  - Example: `x.Name = "Anony"; x.Age = 10; var y = x with { Name="Anony" };`
- Primary Constructors are allowed with Classes using `record` keyword.

Collection Expressions:

- Use while initializing a collection.
- No 'new' keyword.
- No curly braces `{}`.
- Just use open-close brackets `[]`.
- Example: `int[] x = []` or `WriteByteArray([byte)1, (byte)2, (byte)3]);`
- Another: `Span<int> nums = [1, 2];`
- Compiler does the hard work for you.

## OpenAI DotNET: The Official OpenAI Library for .NET

Scott Addie, MSFT Azure SDK Team

Developer Pain Points:

- Ecosystems might be unfamiliar e.g. Python or Node.js are not "build anywhere with .NET".
- REST APIs: Custom wrappers must be developed to call them, and .NET didn't exactly make this simle.
- No SLAs: Some OSS libraries using openAI but not backed by MSFT, blocking adoption by risk-averse orgs.

Solution:

- OpenAI DotNET
- OpenAI library by Microsoft, on behalf of OpenAI, for .NET
- Official NuGet Repo was opened and is now maintained by MSFT
- Azure SDK Team Members are engaged in the development of OpenAI.NET

More Notes:

- All OpenAI's REST APIs will be fully supported.
- Support for latest models.
- Build intelligent apps using C# and .NET best practices.
- Features built-in that devs don't have to write for themselves.
- Designed to make Azure-specific concepts and scenarios very simple.

Features:

- Realtime API (demoed Realtime API for audio).
  - Whisper: Convert audio to text.
- Authentication (with API Key) is required with some systems (e.g. OpenAPI).
  - Azure OpenAI offers keyless auth (Token-based) using EntraID, then RBAC filters for authorization.
- WebSocket instead of REST:
  - Enables duplex communication without REST verb complexities.
- Replacing voice, style, and language are simplified - just replace a few lines of code.

## AI Fundamentals in .NET

Is available in the ML.NET SDK.

Tokenizers:

- Manage context and cause.
- Also a pre-processing step for local models.
- Many are available.

Tensors:

- An abstraction over shaped data.
- Scalers are individual values.
- Vectors are 1-dimentional values such as arrays or spans.
- Matrices are 2-dimentional Vectors.
- Tensor can be Scaler, Vector, Matrix, or multi-dimensional data.
- Simple data sets can be managed simply and directly ("loop unrolling").
- SIM-D recompresses loop unrolling with processing effeciency, but there are still edge cases where code increases due to handling data.
- Tensors handle data processing much more effeciently.
- TensorPrimitives: Introduced in .NET 8.
  - Provides vector-accelerated processing features built-in.
  - Over 200 solutions are built-in to a single line of code.
  - `return TensorPrimitives.Sum(values);`
  - Only operates on raw spans of data.
- `Tensor<T>`: Currently in preview with .NET 9.
  - Define Spans over Tensors for slices of data.
  - Works similar to System.Array but with data specification.
  - ReadOnly* flavors included: `new ReadOnlyTensorSpan<float>(values, [x, y], [a, b]);`
  - _Many_ built-in function members to perform calculations on the shaped data input(s).

Note: Includes support for both .NET and DotNET Framework applications.

## Build a GitHub Copilot Extension

Copilot Extensions:

- Integrations.
- Expand functionality of Copilot Chat.

Can be built three ways:

- Server only: Web service. This has limitations.
- Client only: VS Code Extension for rich interaction.
- Hybrid: Provide a web service and a VS Code Extension that work together. This is much more complicated.

Demo Notes:

- VS 2022 17.12 was used.
- Build GitHub App Copilot Extension, which translates to a ASP.NET Core Web API project.
- .NET 8+ needed.
- HTTPS is recommended.
- Minimal API.
- Dev Tunnels: Requires a MSFT/Github account, can be temporary, but must be public for debugging with Github Copilot.
  - Copy the DevTunner URL that is generated for use later.
  - Allows WRRC between your project and Copilot (in the GitHub cloud).
- Add NuGet Packages: Octokit (latest)
- Authorization:
  - Setup a callback endpoint that Copilot can call to verify user authorization.
- Add two types to support this project:
  - Message with role and content properties.
  - Payload with stream and messages (collection) properties.
- Add a default '/' Post path that accepts X-GitHub-Token with T type Payload payload (using [FromBody]).
- Instant a new `GitHubClient` with new `Octokit.ProductHeaderValue(appname)` in the constructor.
  - Be sure to set an env var that sets an `appname` value e.g. "My-Copilot-Chat-Demo".
  - Instantiate a new Cretentials type and give it a `gitHubToken` as its constructor argument (for instantiation).
  - Add Roles and Content (KVPs) to set up "core messages".
  - Use `HttpClient()` with an `AuthenticationHeaderValue("Bearer", githubToken)` and post the payload as a stream to the "chat completions endpoint".
  - At the end of the endpoing Map, read-in the response (async) and do `return Results...` to push the results to the API caller.
- Github User or Organization Settings must be edited to allow Authorized Github Apps to point to your custom app
  - Might have to create a new one.
  - Name needs to match the local var `appname` (and should not collide with any other Extension name on the Github Copilot planet).
  - Configure the Callback endpoint.
  - Uncheck Webhooks.
  - Permissions: MUST provide Read Only access to Copilot Chat in order for this to work.
  - Permissions: Sharing with the world is possible at the end of the Permissions screen.
  - Enable the Copilot Agent, add the root endpoint of your app, and fill-in other required fields.
  - Run your project so the Callback endpoing exists.
  - Install App (via GitHub account settings).
- Your Extension is selectable using the `@` symbol in the Github Copilot Chat window!
- Open Github Chat in Visual Studio (restart might be necessary), use the `@` to point to your Copilot Extension `appname`, and your Extension will be responding!

_Note_: DevTunnels, when set to temporary, breaks when Visual Studio is restarted. In this case, a new DevTunnels configuration will be required, including the URL settings as configured in Github's Copilot settings.

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
