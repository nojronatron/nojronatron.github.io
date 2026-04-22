# DotNET Conf 2025

November 11, 12, and 13 2025

...Stream of Notes...

## Table of Contents

- [Tuesday Keynote Address](#tuesday-keynote-address)
- [DotNet Improvements in 10](#dotnet-improvements-in-10)
- [GitHub Copilot App Modernization Tools Intro](#github-copilot-app-modernization-tools-intro)
- [App Modernization and Testing Tooling](#app-modernization-and-testing-tooling)
- [AI Agents and MCP Servers](#ai-agents-and-mcp-servers)
- [Building an MCP Server](#building-an-mcp-server)
- [Visual Studio 2026](#visual-studio-2026)
- [ASP.NET Core](#aspnet-core)
- [What's New In C# 14?](#whats-new-in-c-14)
- [Performance Improvements in .NET 10](#performance-improvements-in-net-10)
- [Blazor in .NET 10](#blazor-in-net-10)
- [Aspire 13](#aspire-13)
- [More Copilot and AI-Assisted Coding in VS 2026](#more-copilot-and-ai-assisted-coding-in-vs-2026)
- [Building Intelligent Apps with .NET and Agent Framework](#building-intelligent-apps-with-net-and-agent-framework)
- [Understanding Agentic Dev](#understanding-agentic-dev)
- [Profiling .NET Using Visual Studio](#profiling-net-using-visual-studio)
- [MCP for .NET Developers](#mcp-for-net-developers)
- [DotNET MAUI](#dotnet-maui)
- [Modern Windows Development with .NET 10](#modern-windows-development-with-net-10)
- [Diagnostic Tooling With AI](#diagnostic-tooling-with-ai)
- [Day Two Keynote](#day-two-keynote)
- [Hosting Remote MCP Servers](#hosting-remote-mcp-servers)
- [build smarter agens with redis, .not and agent](#build-smarter-agens-with-redis-not-and-agent)
- [Customizing Aspire](#customizing-aspire)
- [Q and A with Fowler](#q-and-a-with-fowler)
- [Modernizing .NET Apps for the Cloud](#modernizing-net-apps-for-the-cloud)
- [File Based Apps](#file-based-apps)
- [AI Foundry for .NET Devs](#ai-foundry-for-net-devs)
- [Azure App Services for .NET Devs](#azure-app-services-for-net-devs)
- [Best New Features in .NET Test](#best-new-features-in-net-test)
- [The Year in .NET Security](#the-year-in-net-security)
- [Improvements to Linux and Containers in .NET 10](#improvements-to-linux-and-containers-in-net-10)
- [AI Powered Testing in Visual Studio 2026](#ai-powered-testing-in-visual-studio-2026)
- [Thursday YARP](#thursday-yarp)
- [Thursday Decision Records](#thursday-decision-records)
- [Thursday TUIs Are Back](#thursday-tuis-are-back)
- [Thursday Clean Architecture with ASP.NET Core 10](#thursday-clean-architecture-with-aspnet-core-10)

## Tuesday Keynote Address

Host: Scott Hanselman

- Copilot Studio is a Blazor WASM App.
- Bing datacenters have been using .NET 10 throughout the RC process.

Announcing Releases Today:

- .NET 10:
- Performance enhancements.
- C# 14
- VS 2026
- Aspire 13.0
- GitHub App Modernization in VS 2026

.NET Minimal APIs:

- Performance enhancements.
- More Requests/sec (vs. .NET 8)
- Lower memory utilization (Max Working Set MB) (vs. .NET 8)

.NET Goals include:

- Become the fastest platform available.

Host: Maddy Montaquila

- AppHost + CLI.
- Integrations with other code or services.
- Dashboard for one-place view into logs, endpoints, environment, and OpenTelemetry.
- Supports JS, Python, Dockerfiles.
- Cross-language Certificate Trust for cross-platform secure communications.

## DotNet Improvements in 10

Hosts: Maddy, Damian Edwards, and Safia Abdalla

Damian demo:

- Namespace declarations not required.
- Entrypoint static method no longer strictly required in Program.cs
- File-based Apps: `dotnet run <filename>.cs` to run a single-file app!
- `#:` directive: Set build properties, bring-in NuGet packages (and more). e.g. `#:sdk: Aspire.AppHost.Adk@13.00`
- C# 14 Extension Members. Like extension methods but applies to instance methods on top of instance classes.
- `dotnet project convert <file>`: Migrates from File-based to traditional Project Apps.
- Weds morning session with more.

Safia demo:

- Supports OAS 3.1.1 (Open API)
- OpenAPI is moving toward a true JSON superset.
- XML Comments on handlers automatically appear in OpenAPI documentation.
- `[PersistentState]` attribute in Blazor prevents additional fetch operations.
- Generic Model Validation Support. Validate nested, complex types anywhere (including Minimal APIs).

## GitHub Copilot App Modernization Tools Intro

Host: Scot Hanselman

- Dependencies, deprecated APIs, time to refactors.
- Benefits: Improve security and performance, and access to modern APIs and frameworks.
- Modernize with Copilot.
- Included in VS 2026.
- GitHub Copilot Testing Agent for .NET (Currently on Insider's Channel builds).

## App Modernization and Testing Tooling

Hosts: Catchy Sullivan, Brady Gaster

- Demoed a .NET Framework App upgrade to .NET 10 using Modernize With Copilot.
- Supports .NET 8, 9, and 10.
- `@Test` Copilot Agent can analyze a project (or an entire Solution) and build a test project using XUnit, nUnit, etc.
- Will also summarize the work completed with test coverage, quality indicators, and insights and recommendations for how to improve the code (and tests).
- Migrate to Azure Agent: Assessment report provides recommendations for moving the app to Azure.
- Can select containerization, Bicep, Azure SQL, etc.
- Supports Github Actions and Azure DevOps, so R-Click Publish is a 3rd option.

New Hosts: Scott Hanselman, Maria, and Ali

- Build intelligent, Agentic Apps.
- Integrate with Agentic DevOps lifecycle.
- Supported by Aspire.
- Semantic Kernel + AutoGet => Microsoft Agent Framework
- part of ms extensions ai
- Official C# SDK for MCP.

## AI Agents and MCP Servers

Host: Ali

- AI Agents usually have only static data access.
- To gain access to live data, "Tools" allows Github Copilot to call MCPs to access that data.
- MCP Registries: Just like adding NuGet Packages.
- Note: Chrome DevTools MCP exists!
- Authentication: VS 2026 adds r-click built-in way to authenticate with MCP to enable secure comms.
- Project Template for custom MCP Servers! Requires NuGet dependencies to get started.

## Building an MCP Server

Host: Maria

- Agent Framework NuGet Package required.
- Usually, multiple Agents are helpful, adding specialities.
- `[AiFunctionFactory]` attribute.
- DevUI provides visualization of custom Agents. OSS tool.
- Embed AGY Protocol/Chat Clients into a Blazor Application.
  - Agent Packages added to project dependencies.
  - Add 3 lines of code to application to integrate!
- Aspire also shows Agent interactions.

Host: Guarav Seth

- Embracing AI in this new era.
- Decoupling IDE from the dev platform.

## Visual Studio 2026

Hosts: Rachel Kang and Mads T, Visual Studio 2026 team

- Three Goals for VS 2026:
  - Performance improvements: Quicker load and Solution Loading, build, and debug operational cycles.
  - QoL improvements using Fluent UI with improved navigation.
  - Github Copilot capabilities integration, increasing developer productivity and project velocity.
- 5k+ Tickets closed in 12 months.
- 300+ Feature Reuqests implemented in 12 months.
- Extension Migration is enabled: Upgrading from 2022 to 2026 includes currently installed Extensions!
- New, modernized UI with 11 built-in color themes.
- Parallelizes operations like startup, solution load, etc.
- Also leverage backgrounding tasks.
- GitHub Modernize and GitHub Copilot integrated into VS 2026.
- Monthly updates, going forward.
- WinForms Expert Agent to be included in a future monthly update.
- Hot Reload updates early 2026: "Cohosting".
- NuGet MCP included.

## ASP.NET Core

Hosts: Mike Kissler and Safia Abdalla

- Complete modern web framework:
  - Blazor
  - Minimal APIs
  - SignalR for real-time services
  - GRPC
  - Middleware built-in plust customizations
  - Kestrel HTTP Server
- Microsoft Team, Microsoft 365, Copilot, XBox: All use ASP.NET Core
- Focus areas:
  - Simplify building secure apps
  - Integrate observability & diagnostics
  - Targeted performance improvements
  - Address top pain points and gaps
- Passkeys: Replace passwords, are phishing resistant, easy to use, secure by design.
  - Auth templates now include Passkey support.
  - Requires ID DB schema migration (documented).
- Attestation: Not ready yet, to avoid breaking upcoming changes.
- Aspire now supports AspNetCore.Identity metrics.
- Kestrel Memory Pools: Memory release algorithm added to release unused memory to the system.
  - "Memory Trimming"
  - Supports built-in services and custom dev services.
- JSON Deserialization performance (next step from .NET 9 Serialization performance boost) for streaming JSON de/serialization!
- Minimal API Validation! Leverages Extensions and Attributes to implement.
- Server-Sent Events (SSE) for Minimal APIs (for streaming).
- OpenAPI v3.1 support.
- Emit OpenAPI Documents in YAML format.
- JSON Patch with `System.Text.Json`
- "Unauthorized" responses fixes for APIs in Web apps.
  - This is the "Status Code or Login Page" detection solution.
- OpenAPI endpoint definitions in 3.1: `endpoint/openapi/v1.{json|yaml}`
  - Generates response output describing the types.

## What's New In C# 14?

Host: Dustin Campbell

- Nullable reference types: Remove required null checks before assignment:
  - Use `?.` in assignments!
  - AKA "Null Conditional Assignment Operator"
- Lambda Expressions: Param types were required when modifiers used (like 'out' or 'ref')
  - No longer required!
- Field access and Auto properties
  - Auto properties were introduced in C# 3.0, but any modification always requires writing the entire field.
  - Now just stick with `get;` and a `set`.
  - `set` must include the new `field` access keyword.
  - _Breaking change_ especially for DB models that use 'field' as a property name.
  - Leverage `this` or use the escape symbol `@field`.
- Lazily initialized properties:
  - ReadOnlyList type is an example.
  - Integrates `field` keyword and Null Conditional Assignment Operator to enable null-collection at initialization.
- Extension Properties:
  - Extension Methods originally released in C# 3.0
  - Now _very popular_ with libraries built on Extension Methods.
  - Creating a Scalable design to Members is more difficult than mehtods (where `this` parameter is easily added to parameter list).
  - Extension Blocks: Take important bits of Extension Method and move them to the top of the Class, removing `this` keyword.
  - Generic type parameters not needed (due to declaration within the extension block).
  - Static keyword no longer erquired: "Instance Syntax"
  - Becomes the signature used in Instance Syntax, within a static class!
  - Extension Block can include multiple Instance codeblocks.
  - [Exploring Extension Members](https://devblogs.microsoft.com/dotnet/csharp-exploring-extension-members/)
  - Instance Fields are _not_ supported.
  - Setters _can_ be written, but are not included by default.
  - Extension Methods and Properties are now _discoverable_ using Extension Blocks.
- Extension Operators:
  - Add an operator (`-`, `+`, `*`, etc) functionality as an Extension with discoverability.
- Compound Assignment Operators:
  - Modify a type in-place.
  - Not static like usual Operator Overloads.
  - Return Void (changes argument in-place).
- Partial Events and Constructors.
- Unbound generic types in `nameof`.
- [Whats New in C Sharp](https://learn.microsoft.com/dotnet/csharp/whats-new)

## Performance Improvements in .NET 10

Host: Stephen Toub

- [200 page tome](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-10/)
- deabstraction:
  - IEnumerable: ForEach over the collection, but is an abstraction _with costs_.
  - [Enumeration Improvements](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-10/#enumeration)
  - `IEnumerable<T>` causes compiler to generate code to allocate an IEnuerator and implement the `next()` method.
  - The JIT helps to reduce allocations and increase performance in .NET 10!
  - Also, leverage `struct` Enumerator to reduce costs.
- Benchmark.net: Recommended by Stephen
  - Can take a very long time to run.
  - Nieive option is to just use stopwatch and gathering memory and other statistics within .NET benchmarking classes.
- Escape analysis: If JIT can prove an object never escapes, it can allocate it on the Stack (instead of the Heap), freeing up GC pressure, etc.
- JIT improvements apply to other Collection types:
  - Queue
  - List
  - ConcurrentDictionary
  - IEnumerator improvements are key cause for performanc improvements!
- Bit Arrays (built-in type):
  - Collection Marshalling can be used to more efficiently work with bits.
- LINQ (Linq-to-objects):
  - .NET Core 3.x passes information between LINQ operators to short-cut executions.
  - .NET 10.x now "chains" _more_ operations.
  - There are also new methods and optimizations (which Stephen didn't demo).
- RegEx:
  - Since .NET 5, RegEx Engine has seen improvements.
  - RegEx Source Generator first appeared in .NET 7.
  - Focus on making generated code "Atomic", meaning it doesn't have to jump back and forth before either finding the match or shortcut exiting.
  - Other improvements to avoid generating O(n^n) code situations!

## Blazor in .NET 10

Host: Dan Roth

- Security, Observability, Performance, Developer delight!
- Scaffold: Entra ID (dotnet-scaffold) to add auth to existing app.
- Passkeys and WebAuthN built-in to templates now.
- New Diag Tools for WebASM apps:
  - MSBuild props needed in CSPROJ to enable newer diagnostics.
- Fingerprint scripts, then compress and cache them for performance improvements.
- Blazor WebASM resources are pre-loaded (runtime scripts).
- Improved:
  - Hot Reload: The larger the project, the better the improved reload time (maybe?)
  - Blazor State Persistence: Biggest investment! Improves resiliency and scalability. Uses `[PersistentState]` attribute instead of setting prerendering persistent state configuration.
  - Form Validation improvements: `builder.Services.AddValidation()` to use these in Blazor _and Minimal APIs_!
  - Handle Not Found responses
  - Navigation behavor across render modes
  - Interaction between enhanced Nav and Scroll position
  - QuickGrid improvements
  - JS Interop support for invoking constructors, properties, and supplying callbacks
  - Automated browser testing with WebApplication Factory & Kestrel.

## Aspire 13

Hosts: Damian Edwards and Maddy Montiquila

- Aspire is a problem solving framework:
  - Improve, simplify dev loop.
  - Better deployment support.
  - Sits between toolchain and source code.
- Aspire is:
  - Code-first
  - Extensible
  - Observable
  - For Dev and Deploy
- Primary features:
  - Apphost and CLI
  - Integrations
  - Dashboard
- Aspire CLI:
  - CURL-able (native AOT)
  - `aspire update --self` updates all Aspire integrations
    - Includes 'stable', 'staging', and 'daily'
  - `aspire new` templates: Blazor & Minimal API, React (Vite) and FastAPI, Empty AppHost
- Aspire VS Code Extension!
- Can run `npm install` for you as part of AppHost configuration!
- Python and JS debugging support!
  - Polyglot is more than just a template.
  - Aspire is the glue between the languages and frameworks under test.
- Dev Localhost Urls:
  - DotNET 10 feature.
  - Running multiple localhost deployments are all 'localhost' with multiple ports.
  - This provides a way to use an address instead of 'localhost:port'.
  - Prefixes localhost with subdomain naming (from IConfiguration)
  - ASP.NET Core Dev Certificate updated:
    - Now supports localhost
    - Provided to enable "Localhost URLs" with secure HTTP.
- `aspire add container` and `aspire deploy`:
  - Fetches Azure subscription, RG, etc
  - Interactively pick location etc
- [AspireDotDev](https://aspire.dev)
- Aspire MCP is available!

## More Copilot and AI-Assisted Coding in VS 2026

Hosts: Rhea, Jui, Oscar

"Get from an idea to working code using Agent Mode" -Rhea

Demo: Mood Tracking App

- View GH Issues: Select the Github MCP Tool and ask for the list.
- MSLearn MCP Server: Fetches info from MSLearn to apply Agent prompts to write code, add documentation, etc.

## Building Intelligent Apps with .NET and Agent Framework

Host: Jeremy Likness

- Why intelligent apps make sense:
  - Customer experience: Personalization, predictive analysis, NLP.
  - Op Effeciencies: Automation, real-time insight, smart recommendations, recognition of patterns and anomolies.
  - Speed to market: Faster innovation, respond to change and differentiate rapidly.
- .NET AI:
  - Large ecosystem of AI and ML.
  - Cross platform: Python etc.
  - Enterprise grade: Scaling and cloud-native.
- .NET AI Libraries (MEAI)
  - Abstractions and middleware for interoperability and extensibility.
- IChatClient:
  - Ubiquitous interface, same code, regardless of which model or service is used to acess it.
- Generative Pretrained Transformer (GPT)
  - The "GPT" in "ChatGPT" :smiley:

## Understanding Agentic Dev

Hosts: Maria Naggaga, Jeremy Likness

- AI Movement in the last 4 years:
  - Generation to Retrieval to Actions
  - From summaries to reasoning to _agentic actions_
- An agent is:
  - A program
  - Has an input and an output
  - Internally the Agent has an LLM, Instructions, and Tools including MCP
- Workflows:
  - Can be executed whole sale: Kick-off and let it go.
  - Manage step-by-step through the execution.
  - May run for extensive periods of time (days, weeks, etc).
- MS Extensions.AI Eval: In use at MSFT, not ready for release.
- Local LLM Agentic story for Agent Framework:
  - Jeremy used Ollama local models for his demos.
  - So long as its a Chat Client, cloud or local are fair game.

## Profiling .NET Using Visual Studio

Host: Nik Karpinsky, Prin SW Eng Mgr

> Democratize Profiling

- Measure twice, optimize once.
- Discover an issue, get a benchmark, run the benchmark, then optimize code.
- VS 2026 includes Copilot helper to work through profiling workflow.

Steps:

1. Open your project.
2. Create a new Benchmarks project.
3. Next Edit Suggestions can help, but instead go to GH Copilot Chat Agent Mode, select a Model and talk to Profiler Agent with `@Profiler`.
4. Provide any additional context (specific Class, Method, or an entire file).
5. Ask GH Copilot Agent to create a Benchmark.

> Developer still needs to be involved to consider impacts of logging or other calls that might impact the performance but aren't the target of the performance profiling.

Then:

1. Run the benchmark.
2. Ask Copilot to fix the code.
3. Review the code, iterating with Copilot.

> Treat performance as a feature.

Developers need to understand the performance impacts of the changes they are miking.

> Measure, Optimize, Measure!

## MCP for .NET Developers

Hosts: Mike Kissler and Allie Barry

> Enable integrations between LLM Apps and external tools and data sources.

- [Specification](https://modelcontextprotocol.io/specification/2025-06-18)
- Host: LLM/AI Application
- Client: Connects Host to a server
- Server: Services tha provide context and capabilities
  - Tools, Prompts, and Resources.
- Trustworthy actions: Must be consented to.

> The Humun must always be in the loop.

- MSFT partnered with Anthropic to build official MCP SDK for C#/.NET
  - Currently in "Preview 4"
  - Spec is evolving, so won't be 1.0 until Spec is completed.
  - MSFT promises to avoid breaking changes.
  - Multiple MSFT groups and Products already utilize the C# MCP SDK.

How to build an MCP in VS 2026:

1. Install templates: `dotnet new install Microsoft.Extensions.AI.Templates`
2. Create using an MCP template: `dotnet new mcpserver -n {name}`
3. Add Sqlite: `dotnet add package Microsoft.Data.Sqlite`
4. Build the project.
5. Click the Tool Picker :arrow_right: add (+) button and configure the new MCP Server, including command line with arguments (dotnet run etc).
6. Check Tool Picker and select your added MCP Server.
7. Ask Copilot about the MCP Server!

Install other MCP Servers like GitHub, Atlassian, etc.

- Tool Picker integrates Authentication.
- Beware: Limit the number of Tools, otherwise performance will take a big hit.

Prompts and Resources Integrations:

- Tend to save time with prompt creation, etc.
- Prompts can assist with workflows associated with the selected MCP Server.
- MCP Resources: Provide additional context on how to use an MCP Server (the right way).

MCP Roadmap:

- New spec due end of November.
- May SEPs under considtation for next version including: Tasks, better stateless server support, server discover improvement.
- Open process on GitHub and Discord.

## DotNET MAUI

Presenter: David Ortinau

Investments in .NET 10:

- Quality
- Perofrmance
- Simplicity
- Modernization

Contributions:

- Syncfusion (OSS)
- Other Opensource

Presenter: Sam Basu, Developer Advocate, Uno:

- Providing contributions to .NET and MAUI.
- Android bindings and 16KB Support
- Native AOT
- SkiaSharp and WebASM multi-threading
- .NET MAUI Embedding now available in UNO
- WASM integration displays via MAUI WebView component

XAML:

- Global namespaces: Reduce many models and resources by declaring a global XMLNS that points to namespaces (similar to Global Usings).
- Implicit namespaces (Preview): Certain XMLNS are used everywhere so just roll them up and basically define them as a constant in the CSPROJ definition.
- Source Generation: XAML Compilation inflates code during build, and works differently for Debug and Release build.
  - XAML SG (Roslyn Source Generators) XAML -> Roslyn Validation -> C# -> IL -> Visual Tree
  - Faster debug and release builds
  - Consistency between debug and relase
  - Debug the generated code!
  - Also an opt-in feature, enabled in CSPROJ XAML puts files into 'generated' directory

New API: Safe Area Edges

- Control what part of the view is safe.
- Android and Mac supported.
- Windows in near future.
- SafeAreaEdges None: Beed content over unsafe areas.
  - Otherwise, blank areas appear in UI.
  - Must be _specific_ about where safe edges are.

Hybrid Updates:

- BlazorWebView
- HybridWebView
- Invoke JavaScript
- ...others.

Aspire Orchestration:

- Setup AppHost and call `.AddMauiProject()` extension to point to the MAUI CSPROJ
- Microsoft Extensions Helper
  - Meters, Metrics, etc
  - Added to Aspire!
  - Pipe MAUI diagnostics to Debug Output!

[Whats New In .NET MAUI for .NET 10](https://aka.ms/whats-new-10)

## Modern Windows Development with .NET 10

Roy MacLachlan and Michael Hawker

- Large Windows ecosystem
- [WINUI Galler Setup and Information](https://aka.ms/windev)
  - The Encyclopedia of snippets, documentation, design, accessibility, and more!
  - WinUI and WPF both supported!
- Community Toolkit:
  - Yet another gallery of controls and helpers.
  - Supported by .NET Foundation
- MVVM Toolkit:
  - Component Models, DI, and Input defaults.
  - Platform-agnostic implementation items.
  - Commands, Observables, Messenger, IoC, Collections, etc.
- WinUI has been open sourced! Pushed to GitHub in October(?)
- YouTube Windows Developer discussions every month or so.
- AI Dev Gallery:
  - Democratizes AI implementation and use with WinUI.
  - Samples available for app developers to import.
  - Local to the the device (not cloud based).

Microsoft Foundry Local

- New API.
- Easy storage space on local device!
- Minimal memory usage, not cloud based.
- Use WinGet to install `Microsoft.FoundryLocal`
- Foundry commands
- Can list available models including NPU, GPU, and CPU compatible models.
  - Is aware of compatibility with current machine.
- In Csharp add `using` statement and start leveraging FoundryAiModel.

WinAppSdk:

- Moving to version 2.0 soon!

Resources:

- [WinApp SDK](https://aka.ms/winappsdk)
- [WinUI Gallery](https://aka.ms/winuigallery)
- [WinDev (Getting Started Documentation)](https://aka.ms/windev)
- [Widnows Toolkit App](https://aka.ms/windowstoolkitapp)
- Install Foundry Local: `winget install Microsoft.FoundryLocal`

## Diagnostic Tooling With AI

Host: Jonathan Peppers

Debugging:

- Use Visual Studio! F5, Debug -> Widnows -> Show Diagnostic Tools
- CPU Usage Tab is equivalent to `dotnet-trace`
- Memory Usage Tab is equivalent to `dotnet-gcdump`
- Global Tools:
  - `dotnet-trace`
  - `dotnet-gcdump`
  - `dotnet-dsrouter`: Connects to mobile devices, emulators, simulators. Use together with the other tools.
- [PerfView](https://github.com/microsoft/perfview): Great for profiling multi-processes on Windows.

About AI:

- Not yet a replacement - more of a productivity tool.
- AI can unblock "when I'm not the expert".
- AI is good at finding most obvious problems to fix.

Demo: Slow Android App

- Essentially the same experience on other mobile platforms.
- Is a MAUI template with a button that starts a slow process.
- Behavior is slow in Debug mode (but Production mode is faster).
- Start a trace on an App using `dotnet-trace collect --dsrouter android`
  - App must be stopped.
  - dotnet trace displays messages for how to start the app for runtime or startup time attach.
  - Run the App and perform the action that needs to be traced.
  - DotNet Trace dumps a trace file in the current directory.
- Features:
  - Hot Paths
  - Generate with Copilot: Opens Copilot Chat for suggesting optimizations.

Demo: Memory Leaky App

- Leaky Page simply subscribes to an event handler but never unsubscribes.
- Add `GC.Collect();` code lines to simplify memory dump data.
- Run dotnet gcdump and it dumps a file in PWD.
- Use Visual Studio to open the file (the best way).
- Follow the list of items in `Paths to Root` tab.
  - Use the "Show hot paths only" checkbox to focus the results.
- Copilot is not able to open binary files. Peppers wrote an MCP Server that returns text info that Copilot can read. You can too!
  - This allows Copilot to analyze the dump file and provide a fix causing the problem.

## Day Two Keynote

Hosts: Paul Yukenewitz and Scott Hunter

[](https://aka.ms/dotnetconf2025-day2)

How Aspire works with Azure:

- Use `aspire new` on command line.
- AppHost configures resources in Aspire. Moving it into Azure using `aspire add` command.
- `.aspire` directory will store a `settings.json` configuration, and `aspire add` updates the csproj file.
- Deploy with `aspire deploy`: Fires off a pipeline that publishes to Azure, creating resources
- Option: Use `asd up` to deploy Aspire-based solution.

## Hosting Remote MCP Servers

Hosts: Lilly and Anthony

- MCP overview:
  - Connect to external tools, data, and systems.
  - MCP Servers are API wrapped in AI agent consumption format.
  - Transport types: stdio (local), and streamable-http (remote, the focus of this talk)
- Focus will be on Azure Functions, but other options are available.
- AzFunc benefits:
  - Built-in AuthN, AuthZ
  - Fast event-driven scaling 0 to N
  - Serverless, so pay as you go
- MCP Server types compatible with AzFunctions
  - Azure Functions MCP Extension
  - Standard MCP SDKs
- Many languages supported: C#, Java, Python, etc.
- VSCode Command Palette can help Add MCP Server.
  - Produces json config file with 'servers' and 'inputs' properties.
- Add 'host.json' file to tell the host how to find MCP Server (descriptoin, http, and port).
  - Look for 'customHandler' property for this.
  - No other code changes needed once 'host.json' is configured and saved.
- Entra integration for AuthN.
  - Consent request might be made by Copilot during interaction (webUI consent page).
- Also able to integrate Msft Graph, provides Token access to get user information.
- Functions MCP Extensions
  - McpToolTrigger property: Declares a function as an MCP-integrated Azure Function.
  - McpToolProperty property: Declares input items required.
  - API Keys are required using `webhookAuthorizationLevel` in `host.json`. Can be set as an Entra AuthN mechanism rather than anonymous or some other service.
- [Remote MCP Repo](https://aka.ms/remote-mcp)

## build smarter agens with redis, .not and agent

Hosts: Matt Soucoup, Catherin Wang

- Azure Redis Service:
  - REmote DIstributed Server (REDIS)
  - In-memory KVP
  - Azure Managed Redis replaces Azure Cache Redis
- [Azure Managed Redis](https://aka.ms/azure-managed-redis)
- Secure by default:
  - Code time
  - Deploy time
- Aspire has integration with REDIS:
  - `addAzureRedisEnterprise("redis")` automatically provisions instance in Azure
- Microsoft.Extensions.Caching.Hybrid (.NET 9)
  - Supplies 2 levels of caching: Web-server memory primary cache and REDIS cache (secondary)
  - Simple to use, avoiding boilerplate code.
- Output Caching: Header and Footer HTML is stored to reduce server utilization.
- Also see:
  - Note: Microsfot.Azure.StackExchange.Rdis
  - Microsoft Agent Framework for .NET
  - [Azure MCP Redit](https://github.com/redis.mcp-redis)
  - https://github.com/Azure/azure-mcp
- Azure Manager REDIS, Redis Serach module enables Vector Search Cache.
  - Provides fundamental caching, filtering, and hybrid search.
- Cache Expiration is not the default behavior, so use an Azure Function to enable expiration based on criteria/webhook.

Demo: Use REDIS as a Component to an MCP Server

- Setup `mcp.json` file to configure MCP Server
- Sounds like single-line of code enables REDIS for MCP!

Demo: Upload Data Into Redis

- Use an Azure Function, the same way as would be done for a WebApp.
- Redis Data Integration Tool: Utilized for SQL Server or other 3rd party data-oriented tools.
- Redis MCP Servers: Enables Copilot to manage deployment of MCP for Cloud/Azure.

Demo: Use Redis In An Aspire Agent

- Available Features: User Agent, Chat History, Knowledge, Semantic Cache, Distributed Cache, and/or Output Cache (for UI data).
- Deploy Aspire and integrate with your Chat Agent Services.

## Customizing Aspire

Hosts: David Fowler and Damian Edwards

New Features:

- Aspire is code-first, so just write extensions!
- AddDockerComposeEnvironment: New builder extension.
- Declarative resources like Readmes can be written into Aspire.
- Takeaway is to describe how to get and run your app using Aspire:
  - Git clone
  - Aspire Run
  - Done
- New: `AddEfMigrate(app, dbname)` to perform EF DB Migration as part of Aspire startup.
- Aspire supports Rancher, PodMan, and Docker.
- `<IResourceWithConnectionString>`: Formatted connectionstring encapsulation.
- Use `WaitForCompletion(migrationName)` to ensure migration completes before completing launch.
  - WaitFor... can be chained so multiple things can be waited on.
- `WithBuild()`: Once you get the primitive setup, use this to reference your code to do the necessary build steps (like `dotnet build ...`):
  - This supports building other, unrelated Project code!
- Works with File-based Apps!
  - `AddCSharpApp(appname, apppath)`: Currently experimental, coming soon.
- `WithUrls(Action<TRestul>)` to set up how custom app appears in the Aspire Dashboard!
- Add commands that bubble-up to the Dashboard
- `<IInteractionService>`: Enables modal UIs in Aspire Dashboard!
  - Can leverage `<ResourceCommandService>` type wrapper for managing commands.
- Add the Aspire MCP so Copilot can just do the things that are available via AppHost.
  - Will work in concert with other MCPs (Postgres, etc) to discover and use various commands.

## Q and A with Fowler

Geniuses: David Fowler, Maddy Montiquila

Lots of great discussion:

- How Aspire came to be.
- How the Aspire team works through very hard problems.
- Benefits of focusing on a single vertical, learn lessons, then apply to another vertical.
- Benefits of focusing on a single language (integration), learn lessons, then apply them to other languages (integrations).

## Modernizing .NET Apps for the Cloud

Host: Matt Soucoup

> GitHub Copilot App Modernization

- Agent assists with upgrades .NET Framework, .NET Core, to modern .NET
- Modernization is:
  - Assessment of dependencis, CVEs, etc
  - Perform the upgrade languates, frameworks
  - Assess migration (dependencies)
  - Perform the migration (update code)
- Supports: ASP.NET Core, WPF and WinForms, Blazor, Class Libs, Azure Functions, Console Apps.
- Paths:
  - To latest .net
  - New features
  - To Azure
- Manages CVEs discovered in the code:
  - Provides recommended actions to resolve them.
- Can add MCP Servers to increase tool sets, helping migration steps.
  - Could support 3rd party dependencies.
  - Could be custom MCP for other purposes.
  - Could be MSLearn MCP so MSFT best practices are followed.
- References `dotnet-upgrade-plan.md`

## File Based Apps

Host: Damian Edwards

Why?

- Running C# directly is not totally new.
- "C# Interactive", a dialect of C# with semantic differences.
- "CS Script" and "DotNET Scripting": Built on top of C# Interactive dialect.
- MSFT: How do we make this simpler?

Starts with .NET 10!

- Add a 'global.json' to use .NET 10 SDK.
- Add CSharp Extension and C# DevKit to VSCode.
- VSCode settings: Enable File Based Programs :arrow-right: Enable
  - Currently in Preview, will be set in Stable soon.
- Key is in execution: `dotnet run <filename>.cs` :arrow-right: Is now a single-file app!
- Quick to run w/o build delays!
- Add packages to top of CS file!
  - NuGet packages now have a "file based" tab with needed code-line.
  - Adding a Package causes the CLI to run a full MSBuild behind the scenes.
- Can use `dotnet <filename>.cs` instead of `dotnet run ...`
  - Helps with integration with Unix-based systems.
  - "hash-bang" prefix with executable path
    - Ignored on Windows.
  - Supports `dotnet` as single executable argument!
    - Enables directly executing single-file app, so long as the file is marked executable!
  - Can remove `.cs` extension in Linux and just use `./<filename>`
- `#:`: An ignore directive, allowing higher-level processes to handle the file.
- `#:package`: List a dependent package by `name@semver`.
- `#:property`: Set build properties!
- What about `obj` and `bin`:
  - Built C#, not interpreted, so these exist.
  - Base Directory is in appdata:local, that looks the same as a Project directory structure.
- Project File:
  - Completely virtualized. Is generated as an Object in memory instead of a file.
- `[CallerFilePath]` attribute is new.
- `#:project <relpath>`: Reference other projects.
- WebAPI!
  - `webapi.cs`: Pirmary app.
  - `webapirun.json`: New naming format. Ultimate launch file config.
  - `webapi.settings.json`: New naming format. Equivalent to `appsettings.json`.
  - Environment settings are also available.
- `#:sdk <sdk_namespace>`
  - Example: `Microsoft.NET.Sdk.Web` to get all the ASP.NET library goodness!
- `dotnet restore` works, as done `clean`
- File-based Apps will compile-down to Native AOT output using .net publish.
- VS 2026 support not there.
  - Really VS is focused on building solutions, not scripts.
- Focus area:
  - Learners C#
  - Therefore VS Code instead of Visual Studio.
- Playwright scripts:
  - Roslyn Repo: Replacing PowerShell script(s) with single-file app files.
- Redirect artifact output:
  - Set build properties as #: props or Environment Variables
  - Also can be virtual build props.
- Can be run from stdin
  - Pipe it to `dotnet -`!!

## AI Foundry for .NET Devs

Hosts: Bruno Capuano

- AKA "Foundry"
- "...Over 1,900 AI Models with enterprise-grade multi-agent orchestration..." _[Scott Guthrie]_
- Supports generating and producing videos using Sora and other LLMs/Models.
- MS Agent Framework: Can run in AI Foundry, can be based on another existing AI Foundry Agent.
- Scalatility benefits of Azure.
- Tracing support in AI Foundry to monitor AI usage and activity.
- "Add Knowledge": Connect with MCPs and other "Knowledge" connectors to acquire data from Bing, etc.
- Bruno will be posting a Blog Post that explains everything and will include code.

## Azure App Services for .NET Devs

Host: Byron Tardif

.NET 10, Aspire, and New Platform Features!

- Support for .NET 10 is rolling out now.
- Aspire: Support for dashboard!
- New Log Streaming UX, New Instances UX, and New Async-Scaling option.

Notes:

- Create WEb App UI updates Runtime stack w/ .NET 10 (LTS)
  - For Linux rolling out now.
  - For Windows, coming soon.
- Images based on Ubuntu 24
  - WAS Debian
  - Ubuntu servicing is better aligned with .NET team

Deploy App Service _Environment_ with Aspire 13 using Terminal commands:

1. WinGet Microsoft DotNet SDK 10
2. WinGet vscode
3. WinGet Microsoft.azd
4. WinGet Aspire CLI (v.13)
5. Create aspire directory
6. CD into the project
7. Start from template `aspire new aspire-starter`
8. Add Aspire pckg reference: `DotNet Add Aspire.Hosting.Azure.AppService --version 13.0.0-preview.1.25560.3`
9. Use App Service Provider by adding to AppHost.cs: `builder.AddAzureAddServiceEnvironment("bk-aspire-environment")`
10. Setup "external endpoints" (this was unclear)
11. Init and deploy the app: `azd auth login`, then `azd init` and answer prompts, then `azd up`. This creates a `.azure` folder, be sure to gitignore it! `up` decides what resources are necessary to create so Azure can host the App.
12. View deployment in Azure! Note: It includes Container Registry resource (cost considerations).

- Dashboard shares same RBAC access as you have to the WebApp.
  - Supply access to the application, and access to Dashboard will also be granted.

New In Log Streaming:

- Not all traffic coming in is what you want to see.
  - Color-coded log entries help delineate.
- Log types: Runtime and Platform
- Instances: Scale-out instances are listed, to filter all, or just one instance.
- Time-based/lookback period setting (5 to 90 minutes).
  - This is helpful for updating code (inner loop).
  - Production: Set up Log Analytics instead so that Alerts are available (instead of staring at a Log Stream aka "Reading the Matrix").

Scaling:

- Scale Out now supports autoscaling based on rules.

Deployment Slots:

- Being added to Aspire, so slotting new deployments can be configured.

## Best New Features in .NET Test

Host: Jakub Jares

- New view: Interactive, colorful report output.
- DotNet Test Help can detect compatible vs. incompatible test projects.
- DotNet Test can perform retries based on a few types of criteria.
  - Summary displays how many tests were retried.
  - Max Percentage: Causes retries to stop after threshold is reached.
- Azure DevOps/GitHub Actions:
  - Colors highlight failures in logs!
- MSTest v.4 now available on NuGet

Analyzers, Assertions, and Attributes:

- MSTest master package also brings child dependencies that previously had to be added as package references.
- Analyzers can help direct developer to areas where errors in test code exist.
- Not all Analyzers can be Warnings so Analysis Mode was added:
  - In-line warnings at test where issue(s) exist.
  - Analysis Mode can be enabled in the Test csproj file, and this displays Quick Fixes available for rapid test fixing.
- `Assert.ThrowsException<T>` is deprecated. Use `ThrowsExactly<T>` and `Throws<T>` instead.
- New Assertions:
  - Expression assertions with `Assert.That(lambda)`, saving context of code under assertion.
- Conditional Attributes:
  - `[OSCondition(OperatingSystems.Windows)]`, Linux, and `ConditionMode.Exclude`:
  - Only Windows.
  - Only Linux.
  - Not supported on Windows.
  - Good for CI/CD test workflows.
  - Is Extensible so specific cases can be defined to ensure tests run (or don't) when necessary, even in workflow/automated scenarios.
- Performance:
  - Sped up
  - Less memory utilization
- [Test FX Repo](https://github.com/microosft/testfx)

## The Year in .NET Security

Host: Barry Dorrans, Security PM for .NET umbrella and NuGet

Vulnerability Vocabulary:

- CVE: Uniform standard for ID'ing and reporting security vulnerabilities.
- CVSS: Common Vulnerability Scoring System, based on exploitability and impact metrics. High Score != High Risk. Usually aimed at Applications, so Frameworks are scored against _worst possible scenario_.
- CWD: Common Weakness Enumeration. List of weaknesses in software and hardware. Often developer-derived.

Last Year:

- MSRC accepts reports. 84 in last year.
- CVEs: 12
- Bounty paid: $93k
- Documentation _is covered_!
- Not all MSRC reports become CVEs: Not reproducible, not-applicable vulnerability, just a bug not a vulnerability, etc.
  - Sometimes a CVE isn't registered because the fix is applied behind the scenes (bounty is still paid though).
- Only 3 CVE's for ASP.NET in last 12 months!
- Code author is not necessarily the vulnerable code writer to begin with.

Vulnerabilities review (very high level notes here):

- If not actually using SSL: Don't accept payload!
- Differences between Linux and Windows file systems can allow DoS of processes.
  - There are ways to create subdirs so that this vulnerability can be avoided.
  - .NET: use `Directory.CreateTempSubdirectory()` API to be safe on all platforms.
- Always check your dependency directories are correct.
- Input Validation should always be required, even in build scripts.
  - Ignore `Content-Disposition` or ignore the path and only extract the filename to be safe.
- Be very, very careful with code marked as 'unsafe':
  - Lead to a buffer overflow.
  - Fuz your APIs, stay away from code marked 'unsafe', and check your math!
- DoS via poor handling of jagged arrays.
- _Always_ use timeouts to ensure an unfinished session transfer is closed after some reasonable period of time.

[Report security bugs to MSRC](https://aka.ma/corebounty)

## Improvements to Linux and Containers in .NET 10

Hosts: Richard Lander, Chet Husk

> No .net Core on Linux 10 years ago -- but now there are!

- Many Linux distro partners work directly in .NET repos to get things working.
- Packages.microsoft.com (PMC) (Azure Linux and others)
- Enterprise Linux (RHEL, Ubuntu, Snap Store)
- Community Linux distros (arch, centos, fedora, NixOs)
- Base images:
  - Up through .NET 9: Debian. 3 year mainline support. Out of sync with .NET release/support schedule.
  - Starting with .NET 10: Ubuntu. 5 years mainline support.
- Toolset: Clang and others necessary for Native AOT images.
- 10.0-aot: Images are large but work well with multi-stage build and .NET Publish.
- .NET 8/9: Non-root images! Chiseled images! `-extra` images (see docs for details)!
  - .NET Publish selects the correct image based on input.

Ubuntu Demo:

- dotnet SDK publish command compatibility in Ubuntu 24.04!
  - Use dotnet to _create_ containers, then Docker to execute them.
- Images available for multiple platforms (x64, Aarch, etc).

AOT Linux Build on Mac Demo:

- Windows/Mac host system can generate AOT mode build for native Linux using a volume-mount pointing to a Linux container.
- AOT build also works in WSL.

Containerization:

- OCI Container Image Format compliant images.
- Multi-arch publishing knobs:
  - Trimmed, Chiseled, and InvariantGlobalization features.
  - Architecture highlighting during build output reporting.
- Tell DotNet SDK to create a private Registry and publish an app to is, then allow host access via configured port.

Aspire integration?

> Yes, Aspire uses Dotnet SDK customization patterns, however Aspire adds the ability to bring-in Docker-sourced images and customizations, too.

Raspberry Pi OS Support?

> ARM32 and ARM64 are both supported, howeber: ARM32 has a breaking change, so DotNET SDK 8+ required but no Bookworm support. Recommend ARM64 for best compatibility and no breaking change.

[Dotnet and Docker repo](https://github.com/dotnet/dotnet-docker)
[DotNet SDK Container Builds repo](https://github.com/dotnet/sdk-container-builds)
[Container Customizations resources](https://aka.ms/containers/customizations)

## AI Powered Testing in Visual Studio 2026

Host: McKenna Barlow

> MEAI == Microsoft.Extensions.AI library.

Code Coverage:

- Line, Branch, and Method coverage.
  - Can help to discover areas of code that need test coverage.
  - Industry Standard Goal: Get to 70% - 80% coverage in unit tests to minimize risks.
  - Open Test Menu and select Analyze Code Coverage for All Tests to get a coverage report.
  - Add/Remove columns in Coverage Results view.
  - Added Search Filters in Search drop-down.
- Code highlighting indicates covered and uncovered code visually.
- Report Export is stored as XML.
  - Use the Report Generator Tool to view the report.
  - Install using `dotnet install`
  - Report Generator Tool allows drilling-down into report details to get specific coverage area report details.
- Ask Copilot!
  - Copilot explains the issue in Chat, Ask mode.
- Live Unit Testing will automatically update when changes are made to code.

GitHub Copilot Testing for .NET:

- Released to Insiders alongside .NET 10.
- Can generate on a method, file, project, or entire solution.
  - Many, many options here.
- Use `@Test` and pick the project (API etc) to work on.
  - Copilot will create a plan to create and/or add tests.
  - Copilot can add a test project entirely if needed.
  - Tests are generated deterministically (tied to Code Generators).

AI Evaluators:

- "How do we know the AI did a good job?"
- MEAI Evaluation Libraries:
  - Fast Testing, Scalable storage, CI/CD integration with AzDO.
- Reporting Configuration can accept a connection configuration to an Azure AI Model.
- Generate Eval Report to see why a Fluency, Coherence, or Groundedness score is low.
  - Eval Reports are customizable.

## Thursday: YARP

Presenter: Ryan Karg, SW Architect, Blizzard

YARP:

- Developed in C Sharp.
- Based on ASP.NET Core stack.
- Defaults as a standard load balancer.
- Generally, an L7 Proxy with injectable configuration.
- Can be customized to meet specific needs.
- Workflow has destination enumeration, health checks, load balanceing, config customization, health checks, request transforms, session affinity, and HTTP Forwarder processes.
- HttpClient is used at HTTP Forwarder Process to call specific destination server.
- Use `builder.Services` to add to Service Collection.
- e.g. `.AddReverseProxy().Services.AddSingleton<IProxyConfigProvider, ObjectStorageConfigProvider>();` and `app.MapReverseProxy();`
- Custom logic can be pulled from an `IProxyConfigurationProvider` interface to determine proxy behavior.
- `IMemoryConfigProvider`: YARP uses to snapshot configuration and monitor for config updates so it can be implemented in a loop to find and apply the changes.
- Health Checks are available by default with YARP:
  - Are configurable.
  - Includes Circuit-Breaker code.

## Thursday: Decision Records

Host: Sarah "sadukie" Dutkiewicz, Sr. Trainer, NiblePros.

"Understanding why those decisions were made!"

Decision Records:

- Capture why a decision was made.
- Example: Nygard's Template.
  - Title: id + short desc
  - Status: draft | proposed | accepted | superseded | obsoleted
  - Context: Why?
  - Decision: What was decided (with justification)
  - Consequences: What are trade-offs?
  - Notes: Compliance guidance, additional supporting references.
- YMMV: Customize to the team/committee/org/unit
- ADR Format: Architectural Decision Record
  - A standardized way to capture Decision Records.
  - Not just for architecture.
- ADR's can help you _even as a solo team_:
  - Future You will thank you.
  - Context is easily lost without this.

What to capture:

- Based on architectural significance.
  - Structure, architectural characteristics, dependencies, interfaces, and construction.
  - Construction is usually related to implementation, but there are details involved that should be captured.
- "Clean Architecture"
- Non-functional/Architectural significance properties:
  - All of the 'ilities' such as 'securability'
- Dependencies like:
  - ORM vs direct DB access.
  - Document the WHY such dependency was selected.
  - Not sure if needs to be documented? Is probably a dependency.
- Interfaces are at protocol-level and need to be documented in context.
- Construction:
  - Platforms, Frameworks, Tools, Processes

> Avoid capturing business decisions unless they directly impact an architectural decision.

When to capture:

- Before: Draft status, might not have all the details yet, but start an entry with context.
- During discussion: Document as you go so the context is right there to record.
- After decision is made: Depends on how long after it was made.
  - _Still capture it_

Who should capture:

- Software architcts, developers, project managers, ...someone who is good at documentation.
  - Sometimes it is good to distribute this work to prevent burnout.
  - AI is a possible option.

Where to store:

- Document storage.
- Formal document control system.
- Folder on intranet, wiki, etc.
- In a place where everyone that needs them can access them.

How to capture:

- ID the decision to be made.
- Gather _relevant_ information.
- Justify the decision.
- Document the decision.
- Communicate the decision.
  - So stakeholders know what was decided and why.
- Execute on the decision!

Additional Notes:

- Knowledge of related technologies and processes is necessary.
  - Find the SME's that will help determine the possible list of relevant options.
- Decisions can be superceded or deprecated over time.
- "Trade offs" might be a more effective term than "Concequences".
- Obsoleted or Superceded ADR entries should reference a new ADR so chain can be followed if necessary.
- Using AI to create ADRs: Need to be _very specific_:
  - Headings
  - Format
  - Walk the Agent through the decision.
  - Leverage Agents that can categorize and summarize.

> "Do this for yourself!"

## Thursday: TUIs Are Back

Host: Andres Pineda, Sr Dev, Uno Platform Core Dev Team.

> Creating Modern CLI Apps in .NET

Evolution:

- Punch cards
- Green screen/text and keyboard
- Graphic interfaces (e.g. Desktop)
- Web interfaces (document context instead of application context)
- Mobile UI, voice-command device.

CLIs vs TUIs:

- Both: Text base, run within a Console window.
- CLI: Command-line Interface. Text-based, accepts and processes individual commands.
  - Focuses on "Commands"
- TUI: Terminal User Interface. Text-based environment with structured layout using characters and text blocks.
- New `System.CommandLine` .NET library helps with parsing parameters.
- Andres demoed [Spectre Console](https://spectreconsole.net/)
- Toolkit for rich, cross platform UI apps for Windows, Mac, and Linux: [Terminal GUI](https://github.com/gui-cs/Terminal.Gui)
- Use Razor Syntax to create a TUI: [Razor Console](https://github.com/LittleLittleCloud/RazorConsole)

## Thursday: Clean Architecture with ASP.NET Core 10

Steve Smith "Ardalis", Principal Architect, NimblePros.com.

New .NET 10 feature: Run using DNX.

"Everything in software architecture is a trade-off." _[Fundamentals of Software Architecture]_

> "It depends..." -Consultants everywhere.

- Who are you building for?
- What are the 'ilities' that need to be characterised for the architecture?

Context:

- 1990's: "Client - Server architecture".
  - Most Apps all want to talk to the same DB Server (and same DB).
  - Allows for low-overhead change notification!
  - If any client wants to make a change, it has to be aware of other possible client changes.
- 2000's: "Layered Architecture"
  - Tiered: UI, Business Logic, Data Access, DB.
  - Challenge: All layers end up depending on the DB, so testing is difficult.
  - Lack of IoC and SOLID principles.
  - Also: XP gains popularity.
- 2003: Domain Centric Approach
  - Write loosely-coupled applications.
  - Utilize adapters to maintain connections to dependencies (DB, HTTP, etc).
- 2005: Ports and Adapters architecture (Hexagonal)
  - Core business logic is in the core
  - Other logic (App Services, UI, dependencies, tests) plug-in to the core as needed.
- 2009: Onion architecture.
- 2011: Clean Architecture book published.

Clean Architecture:

- First rule: The Dependency Rule.
  - Should flow _toward_ the core/domain, not infrastructure.
  - Usually enforced by a compiler (no circular dependencies).

Core/Domain:

- Pure Code.

Use Cases/Application Layer:

- Commands.
- Queries.
- CQRS.
- Points to Core/Domain layer.

Infrastrucutre/External Concerns Layer:

- Depends on Use Cases.
- Depends on Core/Domain.

Front End Layer:

- Depends on infrastructure.
- Depends on Use Cases.

Process Boundary:

- How to communicate outside of the application:
  - DB
  - HTTP
  - Files
  - Etc

Web Services:

- HTTP to the world.

Template:

- `dotnet new clean-arch -o <name>`
- Clean-architecture layout of projects.
- Adds Aspire.
- Leverages Value Objects (strong custom Types) rather than primitives.

Tools:

- [Papercut SMTP Server](https://github.com/ChangemakerStudios/Papercut-SMTP)
  - Add to project to simplify dev, test.
  - Drop a Container directly into Aspire!
- Dependency Cop
  - Block adding certain namespaced dependencies to Classes in another namespace.
  - Rules for "cross-cutting concerns".

Clean Architecture Critisisms:

- Adding a new CRUD functionality might require updating files in multiple CS Projects.

Resources:

- [Ardalis DotNET Conf Gist](https://gist.github.com/ardalis)
