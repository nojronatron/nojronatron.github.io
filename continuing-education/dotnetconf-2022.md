# DotNET Conf Notes November 2022

Notes taken from live streams and recorded sessions of DotNET Conference, held in November 2022.

## Table of Contents

- [WASM Improvements in DotNet7](#wasm-improvements-in-dotnet7)
- [The State of DotNET MAUI](#the-state-of-dotnet-maui)
- [Container Apps](#container-apps)
- [Azure Functions in DotNET](#azure-functions-in-dotnet)
- [Upgrading from NET Framework to DotNET 7](#upgrading-from-net-framework-to-dotnet-7)
- [Footer](#footer)

## WASM Improvements in DotNet7

WASM => Web Assembly

Key point: Blazor handles all of the DOM Manipulation, enabling development to concentrate on functionality and style.

Runtime provides:

- API Compatibility (browser and external as able)
- Within constrained browser environment
- Small download size

WASM integration in DotNET support Blazor framework.

DotNET enables full-stack webapp deployment using common frameworks and libraries.

New in 7:

- Enhanced debugging: Not the usual debugger because tunnels via JS debug proto in WASM.
- Enhanced debugging: JustMyCode on/off in Visual Studio.
- Enhanced debugging: Debug multi-dimensional arrays even in Hot Reload.
- Enhanced debugging: Actual Call Stack method names now bubble-up to the CallStack view pane.
- Hot reload improvement: Support for editing/changing types and values without stop/restart.
- Enhanced web crypto
- WASM SIMD and exception handling: Single Instructiom Multiple Data.
- WASM AOT support: Ahead Of Time compilation: `dotnet workload install wasm-tools` (or tools-net6 for prior version).
- WASM Experimental tooling: `dotnet workload install wasm-experimental`
- Enahanced JS interop

Enhanced JS Interop Features:

- Strongly-typed by default.
- Optimized for WASM execution.
- No more IJSUnmarshalledRuntim (unless Blazor Hybrid).
- JSImport => JS Functions into DotNET.
- Proper EF 6.0 module utilized in DotNET 7.
- JSExport => Allows calling methods across JS and DotNET. This is an [attribute] to send function returns from DotNET to JS.
- Promise support is included.
- JSHost.Invokeasync => Import JS Modules into DotNet Blazor.
- './dotnet.js' to add library call support from JS to DotNET.

App Project Template Support:

- WASM Browser App
- WASM Console App

Multithreaded Support (preview):

- Browsers usually single-threaded.
- Thread emulation within WASM: `var thread = new thread(()=>{ processing... })`
- Share memory with Shared Array Buffers.
- Requires WASM-enable-threads.
- Not supported in Blazor yet, limited to experimental templates only.

Uno Platform DotNET 7 => Check out uplatform.uno for more info.

Limitation on debugging WASM: Limited to Chromium-based (for now).

WASI: Web Assembly System Interface.

- Allows access to platform the RunTime runs on, in the context of WASM and web-based development.
- Can be containerized to limit impact of possibly hostile code.
- See [wasi.dev](https://wasi.dev/) for details.

## The State of DotNET MAUI

MAUI => *M*ulti-platform *A*pplication *U*ser *I*nterface

> MAUI for DotNET 7 is now GA!

MAUI statistics:

- MAUI for DotNET 6 GA: May 2022
- Growth: 160% YTD
- Faster Rendering and Scrolling.
- [MAUI 7 Performance](https://aka.ms/maui-7-perf)

MAUI Is:

- Built on DotNET Core.
- Evaolved out of Xamarin Apps.

MAUI for dn7 Today:

- MAUI Supports DotNET 7!
- Dev-test-build-distribute-monitor.
- Upgrading from 6 to 7 support is simple (project configuration edit).
- Accessibility in included by default, passing all certifications for an accessible app (1st party app examples: Be My Guide and Hack The Hire).
- Unified .NET with desktop and hybrid offering.
- Native APIs and performance improvements.

Later:

- Xamarin Test support.

Learning:

- New 7.0 feature documentation now online.
- MS Learn has been updated with DotNET 7 features.

New Features:

- Foldable device support (\*.AndoroidX.Window)
- Window Positioning
- Tool Tips
- Context Menus
- Accessibility Improvements

URL Routing:

- DotNET MAUI supports this.
- Overcomes navigation problems between Blazor, Mobile, and Desktop app types.
- Desktop App buttons are _native_ with built-in capability.

About [.NET MAUI](https://learn.microsoft.com/en-us/dotnet/maui/what-is-maui?view=net-maui-7.0)

## Container Apps

How to use DotNET with Azure Container Apps!

Azure Container Apps:

- Build modern app on open source e.g. Kubernetes, KEDA, Envoy, Dapr, etc.
- Focus on apps not on infra: This abstracts-away that complexity.
- Scale dynamically based on events.

What Can I Build with CA's?

- Microservices: Sync/Async communications among small services like with Dapr.
- API Endpoints support.
- Web Apps support.
- Event Driven Processing.
- Background Processing tasks.

Concepts and Terminology:

- Environment: Isolation boundary. Share same vNet (the core boundary), logging, and observability. Supports 1 to n Container Apps.
- Revisions: N per Container App. Allow testing Container App before deployment or for A:B Testing. Usually single revision running at any time.
- Replica: N per Revision. Inner-arrows pointing from Revisions to the replicas standing by.
- Container: N per Replica. Side-car container: Runs in same Replica along with a "primary" Container.

Ingres:

- Envoy is used to route ingress traffic to single or multiple Revisions.

Use the Publish Tool in Visual Studio to deploy new, or to an existing Container App.

- Application code must exist in an accessible repository e.g. GitHub.
- Must also "push generated workflow" (the yaml file) to the GH repo.

Container Apps can talk directly with each other when they are in the same Environment (the same vNet), so making an API private or public is not necessary for back-end calls!

## Azure Functions in DotNET

DotNET 7 support in Azure Functions.

DotNET Framework support in Azure Functions v4.

Event-driven, serverless compute service. _[MSFT, DotNET Conference]_

Built on top of Web Jobs.

- Triggers and hosting models will be different though.
- Some HTTP scenarios might be better suited for Web Job consumption model vs. Az Funcs.

Integrated programming model:

- Various triggers and bindings
- Define when envoked
- Define what data is connected

End-to-end development experience:

- Build and debug lcoally
- Windows, MacOS, and Linux

Hosting options flexibility:

- Choose your environent.
- Dev experience is the same in each.

Fully managed and cost-effective:

- Automated and flexible scaling.
- Scaling based on workload volume.
- Focus on adding value.
- Reduced need for dev to manage infrastructure.

Tool chain:

- VS 2022
- VS Code
- Az Funcutions core tools

CI-CD:

- GH Actions
- Azure Devops

Isolated Worker Process:

- Decoupled from host .NET versions.
- Dependency Injection support.
- Middleware support.

[Azure Functions DotNET Isolated Guide](https://aka.ms/af-dotnet-isolated-guide)

Performance enhancements:

- Durable functions.
- SDK Type Bindings: SDK Abstraction with performance benefits.
- Enhanced HTTP Trigger: Access to underlying request in-proc with additional out-of-proc info.

Use Attributes in your code to assign values and configuration for an AzFunc call and response in your API.

- `HttpTrigger()`
- `BlobInput()`

Migrating: Functions 3.0 and 1.0 can be migrated to v4, and guides are available from MSFT.

Roadmap:

- Closing the gab between in-proc and isolated proc models, then will stop releasing in-proc models.

## Upgrading from NET Framework to DotNET 7

I have a WPF application that was built using DotNET Framework 4.x, and I want to upgrade it to DotNET 7.x (or at least DotNET 6.x LTS) so that I can continue to learn, as well as grow the project into new capabilities of DotNET and C#.

An additional goal of migrating to the latest SDK, is to ensure application compatibility and support with existing and future platforms, especialy Windows, but including Linux (especially with DotNET 6+ where Linux apps can be built and deployed in a Windows SDK environment).

There are [differences with WPF DotNET](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/migration/differences-from-net-framework?view=netdesktop-7.0).

DotNET 7 Upgrade [WPF](https://aka.ms/dotnet/upgrade).

How to [upgrade WPF Desktop App to DotNET 7](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/migration/?view=netdesktop-7.0&WT.mc_id=dotnet-35129-website).

### Workflow Recommendation

- Identify dependencies: Some could be upgraded, others removed and/or replaced completely.
- Upgrade project and NuGet references: Target the net project SDK.
- Upgrade source code and other project assets: Tools exist to help along the way.
- Test and Deploy: Unit testing is necessary and integration and runtime testing are too.

#### Dependencies

Dependencies could include:

- .NET APIs
- NuGet packages
- Project-to-project dependencies (references)
- Loose binaries

#### Upgrade Project and NuGet References

Project configurations are in the new SDK format, which is not compatible with DotNET Framework SDK project definitions!

- Upgrade in-place
- Upgrade incrementally

#### Upgrade Source Code and Project Assets

- Use the DotNET Upgrade Assistant
- Incremental Migration Tooling can help

#### Test and Deploy

- Some changes are only visible at runtime
- Cross-platform migration will require additional integration testing: Live/Runtime testing

### Upgrading In Place

- Works for projects updated in-place to DotNET Standard or _multi-targeted_ between DotNET 7 and DotNET Framework.
- Fastest path to full migration.
- Prevents duplicate code.
- Recommended for non-ASP.NET scenarios (WPF, Console, etc).
- DotNET Upgrade Assistant can help with this scenario.

Suggested workflow:

1. Make a tree map of the projects in the Solution.
2. Map-in the dependant projects.
3. Map-in the dependent Libraries.
4. For every leaf node (has no child dependencies), start an upgrade there.

Note: Multi-targeting is an option.

Microsoft highly recommends this option whenever possible (except ASP.NET due to differences in ASP.NET Core) and very large Libraries.

### Side-by-side

- New project(s) created and implementation is moved-over gradually.
- Build and deploy can continue throughout migration.
- Recommended for ASP.NET or very large class libary project/solutions.
- [VS Extension for incremental migration](https://devblogs.microsoft.com/dotnet/migrating-from-asp-net-to-asp-net-core-part-4) is an available tool.

1. Create a new version based on the target SDK.
2. Migrate individual libraries to migrate over.

A reverse-proxy is used to manage directing requests to the original ASP.NET, or the new ASP.CORE app, on a feature-by-feature basis.

Visual Studio Extension "YARP" exists to help migrate legacy ASP.NET Project to ASP.NET Core within the VS IDE.

- Not a be-all, end-all tool.
- Will help accelerate migrations.
- Some manual effort will still be required.

There are "Adapters" for System.Web that help migrate to ASP.NET Core, and move away from legacy functionality.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
