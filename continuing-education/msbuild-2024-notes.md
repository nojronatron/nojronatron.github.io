# MSBuild 2024 Notes

Microsoft Build is a yearly conference aimed at .NET developers and focuses on Visual Studio, languages like C#, F#, and Visual Basic, developing solutions using Azure or Microsoft 365, and updated information on .NET.

MSBuild took place on 21 May through 23 May, 2024.

## Table of Contents

- [Sessions I Could Not Attend And Want To View](#sessions-i-could-not-attend-and-want-to-view)
- [Infusing .NET Apps with AI](#infusing-net-apps-with-ai)
- [Developer Experience Improvements in Windows](#developer-experience-improvements-in-windows)
- [DotNET API Development End-to-End](#dotnet-api-development-end-to-end)
- [How To Quickly Build a DotNET WPF Dashboard Application](#how-to-quickly-build-a-dotnet-wpf-dashboard-application)
- [Modern Full Stack Web Development with ASPNET Core and Blazor](#modern-full-stack-web-development-with-aspnet-core-and-blazor)
- [Running NET on the NES](#running-net-on-the-nes)
- [Create Superior Experiences with WinUI and WPF](#create-superior-experiences-with-winui-and-wpf)
- [Unleash The Potential Of APIs With Azure API Management](#unleash-the-potential-of-apis-with-azure-api-management)
- [Highly Technical Talk - Hanselman and Toub](#highly-technical-talk---hanselman-and-toub)
- [Zero To Hero - Develop Your First App With Local LLMs On Windows](#zero-to-hero---develop-your-first-app-with-local-llms-on-windows)
- [Windows Subsystem for Linux Your Enterprise Ready Multitool](#windows-subsystem-for-linux-your-enterprise-ready-multitool)
- [Whats New In C Sharp 13](#whats-new-in-c-sharp-13)
- [Level Up With DevBox](#level-up-with-devbox)
- [AI Safety and Security Fundamentals](#ai-safety-and-security-fundamentals)
- [Enterprise Class NGINX Plus Without Operational Toil](#enterprise-class-nginx-plus-without-operational-toil)
- [Scott and Mark Learn AI](#scott-and-mark-learn-ai)
- [NET Aspire Dev On Any OS with VS Family](#net-aspire-dev-on-any-os-with-vs-family)
- [Demystify Cloud-Native Development with NET Aspire](#demystify-cloud-native-development-with-net-aspire)
- [Build and Deploy to Azure with GitHub](#build-and-deploy-to-azure-with-github)
- [Building Custom Copilots with Copilot Studio](#building-custom-copilots-with-copilot-studio)
- [Keynote - Wednesday](#keynote---wednesday)
- [Extend Microsoft Copilot Using Copilot Studio](#extend-microsoft-copilot-using-copilot-studio)
- [Maximize Joy Minimize Toil With Greater Dev Experiences](#maximize-joy-minimize-toil-with-greater-dev-experiences)
- [AI Everywhere Breakout Session](#ai-everywhere-breakout-session)
- [Imagine Cup Finals](#imagine-cup-finals)
- [Keynote - Tuesday](#keynote---tuesday)
- [Resources](#resources)
- [Footer](#footer)

## Sessions I Could Not Attend And Want To View

- [ ] Build Apps From The Cloud With Microsoft Dev Box, Visual Studio, and More.
- [x] Developer Experience Improvements in Windows.
- [ ] Accessibility In The Era Of Generative AI.
- [ ] Building Copilots - Key Lessons And Best Practices.
- [ ] Deploy, Test, And Run Apps With Azure Deployment Environments.
- [x] Inside Microsoft AI Innovation With Mark Russinovich.
- [ ] Start Building Your Next App Now With MongoDB Provider For EF Core.
- [x] Infusing Your .NET Apps With AI: Practical Tools And Techniques.
- [x] .NET API Development End-To-End.
- [ ] Enhancing .NET MAUI: Quality, Performance, And Interoperability In .NET 9.
- [x] How To Quickly Build A .NET Dashboard (focused on WPF, MVVM and related best practices and UI design).
- [x] Modern Full-Stack Web Development With ASP.NET Core And Blazor.

## Infusing .NET Apps with AI

Speakers:

- Luis Quintanilla, Sr. Product Manager
- Stephen Toub, Partner Software Engineer, MSFT
- Vin Kamat, Principal Architect

### One Liner To Incorporating AI

Semantic Kernel:

- Provides services to do text completion and suggestions.
- Provides plugability to various language models.
- Includes Helpers to bring-in to .NET Apps as a 1st Class Citizen.

Code:

- `Kernel kernel = Kernel.CreateBuilder()`
- Various dot completions: `.AddOpenAiChatCompletion()`, `.Build()`, etc.
- `kernel.InvokePromptAsync()`: This is a primary actionable method for processing input.

Language Models:

- Start completely stateless.
- ChatServices like `IChatCompletionService` classes will enable maintaining state using a Chat History.
- Can add classes with methods marked as `[KernelFunction]` to invoke functionality. Use `KernelPlugin` to "import" the custom kernel function, then add to the Prompt Execution settings to allow that custom kernel function to be used by the Kernel.
- The AI uses this configuration to "Ask for" execution of the custom method, then uses the output of the method execution (tokenized, of course) to generate a response.

General Comments:

- Libraries are integrated into the .NET Ecosystem.
- Enable Logging (such as the Builder Services AddLogging() function) to enable watching the call/response of Semantic Kernel and custom imported methods.
- Various services in configured within ConfigureHttpClientDefaults to redact private information, enable Polly retries, etc.
- Use your project's existing DI container to enable Semantic Kernel functionality!
- Integration with Aspire and Open Telemetry, and Semantic Conventions for AI (a Standard in preview mode).

## Developer Experience Improvements in Windows

Speakers:

- Kayla Cinnamon, Sr. Product Manager, Dev Home and PowerToys
- Sharla Soennichsen, Product Manager, Dev Home and Machine Configuration

Team Products:

- Windows Terminal
- WSL
- Dev Home
- PowerToys
- WinGet

> "Tools focused on keeping developers within their flow"

### PowerToys Updates

PowerToys Projects:

- Loads an existing Workflow.
- Remembers a window layout to quickly get up and running as you left it.
- Supports different screen resolutions and multi-monitor.
- Customize _the way apps open_.

### Dev Home New Features

Your Development Control Center:

- Extensible: GitHub, Azure DevOps.
- Connect to GitHub and other Developer or Azure Accounts.
- PowerToys integration! Hosts File Editor, Registry Preview, and Env Vars Editor (to start, more on the way). MSFT _wants OSS participation and input_.

Dev Home Environments:

- Multple Environment storage and selection screen.
- Single-pane access from within Dev Home.
- Launches DevBox preconfigured with needed tools.
- Create new environments for Hyper-V, Dev Box, and perhaps more in the future including Ubuntu, Win10 MSIX Packaging images as a base.
- Configure the Env Vars for an existing Environment to clone an existing public repo, select Apps to include, etc.
- Generate Config File: Specify ideal state wanted for an environment/machine and store as a YAML file. Great for duplicating to other machines!
- Integrated with PowerShell DSC Library, so will have some delay in loading summary view or code view as they are pulled from the marketplace.
- Adding Source Control integration into File Explorer. Git details are added to Details View, and there is a Git-Like status display at the bottom of File Explorer window.
- Windows Customization: File Explorer Settings, Dev Drive Insights, Windows Developer Settings, and Quiet Background Processes.
- Dev Drives: File type based on REFS to provide IO-heavy performance improvements.
- Export Application settings: Pass-in file, resourceID, yaml to `winget configure export` and outputs a DSC YAML.

### WinGet Configuration

- Winget configure YAML: Reads-in the YAML file and creates a Windows Sandbox, executing YAML instructions similar to GitHub Actions/Azure Pipelines, but local.
- Winget Install: Updates current environment PATH when installing packages e.g. `winget install git.get` and then git commands will function without having to restart Terminal!
- `sudo` enables executing commands that require Administrator privileges without elevating the current (or another) Terminal instance.

### Command Line Improvements

- Inner Panes: Spawn from an existing Tab.
- Snippets: Commonly used commands can be pasted to the current shell/Posh/Terminal.
- Dev Home: When Terminal Starts setting to customize Terminal launch look and behavior.
- Terminal Buffer Content Restore: If closing

### Sneak Peeks

Visual Studio Extension Windows Sandbox:

- Can be targeted by VS 2022 to run within the Windows Sandbox environment.
- Supports redeploy after making code or dependency fixes.

### Resources

Root URL aka.ms:

- devhomedocs
- powertoys-docs
- terminal-docs
- winget-docs

Root URL microsoft:

- devhome
- powertoys
- terminal
- winget-cli

## DotNET API Development End-to-End

Presenter: Sayed Hashimi, MSFT

Essentials of building Robust APIs:

- Design
- Create
- Test
- Deploy

> Implement seamless API Development Lifecycle

### DotNET API End-to-End Overall Notes

Things Sayed did:

- Chose ASP.NET Core WEb API Template.
- Enabled OpenAPI Support.
- When NOT selecting MVC Controllers, just use Minimal API Endpoints.
- Use VS Scaffolding to pick API with R/W Endpoints using Entity Framework, to point to initial related class models. Select the Context class fo rhte Model Class. Select an existing or nrew Endpoints Class and DbContext Class. Select a DB Provider like SQLite to get basic CRUD operations.
- Note: Scaffolding is a starting point, not final code! It is up to the developer to edit the code to make it purposed for the project/task at hand.
- Use VS Scaffolding to pick API with R?W endpoints using Entity Framework, to point to additional, releated classes.
- Endpoints Explorer: Display all existing endpoints. Used for all static endpoints only. Dynamic endpoints will _not_ be discovered until the project has been built and run.
- Seeded data by customizing the DbContext Class with custom private method(s) to populate with data.
- Connected Services UI: Add and configure EF Migrations.
- Endpoints Explorer can generate requests for testing! It leverages the `http request` package for simplified request generation and usage.
- Environments: JSON file that defines dev, staging, and other environments using JSON Key-Value pairs. Secrets can be accessed from here (plain text, encrypted, or Azure Keyvault) via the Secret API (accessible within Visual Studio, but not checked-in to repository). User-specific settings can be defined within an environments file ending with `.json.user`.
- Switch Endpoint Explorer HTTP request context to different Environments using the drop-down in the top-right corner of the HTTP Request window. Request having Environments set up as in a previous bullet point.
- `httpbin.org/anything`: Echos your HTTP Request, args, data, files, form, headers, json, method, origin, and URL in a response to the calling client.

## How To Quickly Build a DotNET WPF Dashboard Application

Speaker: Greg Lutz, .NET UI Control Product Manager, Mescius Inc.

### Dashboard Considerations

- Used to gain situtational awareness.
- Provide time-based, insightful reports.
- Data visualization, aggregation (totals by group), filtering, drill-down, and animations enhance dashboard comprehension and usability.
- No data entry or processing, simply visualization.

### Chosing a Platform

WinForms:

- Traditional Windows library.
- Difficult to customize.
- Not very MVVM friendly.

WPF:

- Traditional Windows library.
- WinForms +++!
- Scalable with XAML, for portability to WinUI and MAUI (also Xamarin and others).
- Styling and data binding is better developed.
- DirectX performance enhancement.
- Scalability enhancements.
- Made for use in MVVM paradigm.

WinUI (Win 11+):

- Latest WIndows Store style Apps.
- Not as desktop friendly.
- Very new.

### Dashboard Structure

- MVVM: Separate business and application logic from user presentation layer.
- Notifications are sent _up_ from the Models to the ViewModel to the View.
- Data Bindings and Commands are sent _down_ from the View to the ViewModel to the Models.
- Avoids "code behind" (Jon ed: It is arguable that ViewModels are also tightly coupled to their Views).

### Architectural Notes

- Utilize INotifyPropertyChanged.
- Implement basic functionality in Models to expose data like summing data or returning a product or ratio from the Model data itself.
- Use scalable `<FlexGrid />` elements for simple, flexible viewport/screen sizing (responsive design).
- Filter results from within ViewModel Properties to keep the ViewModel clean and to simplify Data Binding and Notification via `INotifyPropertyChanged`.
- Charts and Gauges using "Component 1 WPF Libraries": FlexChart, FlexPie, BulletGraph?
- Dynamically Bound Collections (e.g. `List<dynamic>`) are used to generate Pie Chart comprised of model data from different Types.

### Mescius Reference

Nuget: Component One aka "C1" from Mescius Inc.

## Modern Full Stack Web Development with ASP.NET Core and Blazor

Presenter: Daniel Roth, Principal Product Manager, MSFT

### ASP.NET Core and Blazor Overview

- Full stack web UI.
- Updated with .NET 8.0!
- Server-side: Handle requests, access resource, and generate HTML.
- Client-side: Handle user interactions, access client resources, update the UI.
- Component-based rendering model.
- Client-side interactions are possible via same Components.
- C#, Blazor, and a unified build system!

### New Blazor WebApp Demo

- .NET 8 LTS Template enables quick new-project setup.
- Hot-Reload to view changes client-side in real time.
- C# Class annotations are supported.
- VS Can scaffold Razor Components to generate pages and other supporting components and adding an ORM such as Entity Framework!
- Entity Framework Migration support.
- By default, pages are statically rendered at the server (SSR). Use `Interactive Server` render mode to allow UI-events to be sent between client and server (SignalR?).
- Built-in `<Paginator />` component enables built-in pagination. Set the Paginator properties in the `@code{}` block e.g. ItemsPerPage.
- `<ColumnOptions />` component enables binding events and data for filtering results.
- `_imports.razor`: Add `@usings` and `@attribute [Authorize]` for _all pages_ within the app.
- Advanced Render Modes, `<QuickGrid />` Component, Monitor circuit activity, Improved Authentication (over .NET 6), Client interactivity per Component or per Page, Streaming rendering, enhanced Form handling, and auto-select render mode _at runtime_.
- WASM (Web Assembly): Jiterpreter, Hot-reload Components, SIMD and Exception handling enabled by default, CSP compatibility, Webcil packaging.

### Authentication

1. Scaffold a new item.
2. Select Authentication.
3. Add Blazor Identity and point to a new or existing SQL-based data store.
4. Setup "core identity" for use. This generates Razor Files implemented in Blazor to support login, authorization, and logout.
5. Add migrations for both the Identity Store and any existing DBs to the Service Dependency using the UI elipses menu on the Connected Services view.

Remember: Registration will use an auto-authorize flow, that should be replaced with a real 2FA flow.

### .NET Aspire With Blazor

- Built with Blazor and Fluid Blazor Components.
- Framework for building cloud-ready Blazor Apps.
- Logs, Traces, Environment Configurations management and insights.

### Bonus Blazor: AI for Apps

Drop-in .NET "Smart Components"!

- Dan demoed a Blazor App to help describe this feature using a "Smart Paste" button that took email plain-text and filled-in a form from that content.
- Demo component: `<SmartPasteButton />`
- Another demo revolved around HR tasks, where a Smart TextArea where appropriate email responses can be generated.
- Demo component: `<SmartTextArea />`: Generates suggestions based on policies.
- Semantic Search: User types data into a Form and Semantic Search provides suggestions from Cloud-based or Local SLMs.
- .NET Smart Components are in _Experimental_ stage but MSFT wants feedback. Check out [dotnet smart components home](https://aka.ms/dotnet/smartcomponents).
- Support for MVC and RazorPages.

### ASP.NET and Blazor Key Takeaways

Scaffolding: Create a model and use the Scoffolding tool in the Add Item submenu to generate front-end, back-end, and ORM code!

Fast Development and Experimentation: Blazor can be used to rapidly trial-run new ideas. Once the project has been fleshed-out and is ready for more formal development, Blazor can again be used as an Enterprise-ready or Cloud-ready full-stack framework.

User State: Remember that Blazor maintains User State while running on Server-Side. If the connection is broken (i.e. the server service restarts) that data will be lost, causing a jarring end-user experience.

Focus for .NET 8:

- Quality and Fundamentals.
- Fills Blazor WebApp experience gaps.
- Blazor Server improvements.
- Optimize page load and startup time.
- Improve developer experience.
- SSR performance, Static Server rendering from interactive, detect current render mode, enhanced navigation in persistent component, declarative models for serialized or prerendered state, Templating for MSFT Entra authentication with tooling
- WebSocket compression, distributed tracing, and improved reconnection logic.

_Note_: Keep an eye on these for the .Net 9.0 release party coming in Fall 2024.

_Note2_: Dan demoed an example of improved Reconnection Logic in .NET 9 preview vs. .NET 8.0.

## Running .NET on the NES

Speaker: Jonathan Peppers, Principal Software Engineer, .NET, .NET MAUI, MSFT

General Notes:

- The NES was _not_ powerful by today's standards: 512kb per cartridge!
- Assembly code is a core, historical language.
- Learning about MSIL and AOT compilers.
- `dotnet new nes` :astonished: Regular net8.0 package, using `dotnes` NuGet Package.
- Emulator Jon used: ANESE
- Requires a set of 'image data', made up of `bytes`.
- `dll`: Class library output.
- `nes` file: ROM output that the emulator consumes.
- Jonathan started by reducing the scope to get 'Hello World' working. No debugger, no GC, no base-class libraries, no classes nor methods! No compatibility requirements, either.
- How does this work? C Sharp compiler produces MSIL (like usual), and then the 6502 Assembly is produced using an MSBuild Task.
- JIT: Just in time compiler, since .NET 1.0. Loads MSIL and transpiles into machine code on-the-fly.
- AOT Compiler: Mono does this, compiling MSIL at build-time.
- iOS and Mac Catalyst _do not run a JIT_. Provides faster startup.
- Native AOT: Introduced .NET 7 for Console Apps. .NET 8 enables ASP.NET, and iOS. More coming in .NET 9.
- 8-bit Workshop tool: Browser-based IDE that includes assembly and execution preview.
- Remember: Games require a run loop, so a `while(arg)` must be included at the end of the code, otherwise the system abends.
- Had to understand the `*.nes` file format.
- Trainer: A special area of ROM where developers could change starting properties like game level, player invincibility, etc.
- Header must be written using a binary writer such as `System.Writer(char)`.
- CHR_ROM: Memory areas where characters were drawn, and tinting and rotating were used to set images.
- 6502 Instruction Set was shared with Apple II, Commedore, and others. _Note_: MSIL instruction set is _much larger_!
- String Tables: An address that identifies a cell in a table with strings that can be referenced.
- Tool: ILSpy allows viewing the Metadata, References, and Resources.
- Jon leveraged ENUMs of the NES Instructions so he could easily call them.
- Endian: The NES is Little Endian, so smaller letters have lower value encodings.
- MSBuild has Targets (XML) and Tasks (C#, generally).
- MSBuild Target: Defines what is run _after the build_. MSBuild properties are marked with `$(variable)`. Inputs and Outputs are set. Item Groups like `@(item)` work like collections of references.
- MSBuild Tasks: PropertyGroup encapsulates `<RunCommand>`, `<RunArguments>` and `<RunWorkingDirectory>`. Tasks are often used for builds that require script executions for customizations or specific CI-CD tasks.
- `neslib`: There are about 44 methods that had to be transpiled.

Jonathan's Thought Process:

| Developer Experience                                | Hard Part                                               |
|-----------------------------------------------------|---------------------------------------------------------|
| Write a C Sharp reference assembly for neslib API   | Learn NES binary format, write header in C Sharp        |
| dotnet new nes project template                     | Just understand enough to write 'Hello World'           |
| MSBuild tasks and targets for dll to nes            | Use System.Reflection.Metadata to convert Main() to 6502 assembly |
| Write unit tests and verify expected output         | Write Super Mario is C Sharp                            |

Advice for doing this yourself:

- use 8-bit workshop.
- learn a little bit of C.

Project GitHub:

- [DotNES GitHub](https://github.com/jonathanpeppers/dotnes).
- To get going use `dotnet new install dotnes.templates`.

## Create Superior Experiences with WinUI and WPF

Speakers:

- Ranjesh Jaganathan, Engineering Manager, WinUI Team, MSFT
- Niels Laute, Sr Software Engineer, Windows Team, WinUI, Community Toolkit, PowerToys, MSFT
- Pankaj Chaurasia, Engineering Manager, Client Platform, WPF

MSFT Client Dev Investments: Windwos Native, Cross Platform Native, Hybrid, and Web!

What is a superior app experience?

- Many things, according to MSFT, partners, and other WinUI and WPF developers.
- App reviews/ratings also help define what is good/superior.
- Design: Modern, Windows-app designs.
- Performance:
- OS Integration:

Demos: Contoso Camera Manager and Contoso Studio.

Contoso Camera Manager (WPF):

- Device settings on the left, and pictures gallery on the right. There are also a Device and About menu items under the Title Bar.
- Modernization means: Look and feel,
- Import the Fluent Design resource 'Fluent.xaml'.
- WPF imports Accent Colors as set in the Control Panel! Removing specific styles enables 'Fluent Design' to do the styling for you! Just add the Fluent properties using the style property `DynamicResource` value on the appropriate element.
- WinUI 3 Gallery tools _can also be applied to WPF projects_.
- WPF will no longer have some (legacy) WinForm dependencies in .NET 9+
- `Packaging` puts your App in your Start Menu, and Hot Reload is still enabled for dev and debug!
- `AppNotificationBuilder` enables creating a simple Windows Notification with about 6-7 lines of code!
- ShareSheet: Enables sharing items to/from your WPF App (similar to mobile). Package.appxmanifest must be edited to enable ShareSheet as a ShareTarget. `ShareDestination` must be added to share _out_ from your app.

> Add fluency to a WPF App simply and easy, using .NET 9 and the WinUI 3 Gallery Tools and the new APIs.

Contoso Studio (WinUI 3 and WinAppSDK):

- Pages navigation on the left.
- Light/dark mode.
- Settings control in the BLC.
- Upper and lower main window area with statistics in the upper area, and content w/ actions (delete) in the lower area.
- Missing features too!
- Windows Store uses _all custom controls_ and the "fluid design system".
- [WinUI 3 Gallery](https://apps.microsoft.com/detail/9p3jfpwwdzrc?amp%3Bgl=US&hl=en-us&gl=US): Contains many tools and guidance including iconography, typography, accessibility and more! Color fill, stroke, background, etc tools are in there too!
- WinUI 3 Gallery Spacing Page: New! Advice on various spacing concepts and practices.
- `<Window.SystemBackdrop>`
- Cards are just Theme Resources from the WinUI 3 Gallery.
- Creating a custom Icon and TitleBar requires a lot of builerplate code. New Control `TitleBar` control will be available in 1.6-Experimental.
- Activating/Deactivation the window: Changing the background color (slightly) makes it apparent that the app is selected, just like in Windows.
- `<ItemsView>` is being rebuit from the ground up. Attached Property `Layout` can be set with defining Resources. It is built out of many other things including ITemsRepeater, ItemsSource, Layout (virtualizing and non-virtualizing), and verious collection change animations. ItemTemplate manages recycling. Stack, UniformGrid, and LinedFlow are also related to the collection of things here. ScrollView, ItemContainer, Various interactions, keyboarding, and accessibility, are also included.
- `<SelectorBar>`: New, drop-in replacement for `<ItemsView>`, that enables native aspect-ratio for images, and provides changing views of the child items.
- Virtualizing and non-virtualizing Layout: Everything is already loaded regardless of where the view is, unless it is virtualized, in which case items are loaded just-in-time for the actual Viewport (Realization Rectangle). Items that fall out of the Realization Rectangle get recycled automatically.
- Helpful tools: WinUI Performance Toolkit and XAML Frame Analysis Plugin for WPA.

> Fluent Design system and WinUI Gallery were used to help design the demo app.

## Unleash The Potential Of APIs With Azure API Management

Speakers:

- Nima Kamoosi, Sr Director, Azure Team, MSFT
- Pierce Boggan, Product Lead, API Center & Copilot Dev Experience, MSFT
- Julia Kasper, Product Manager, Azure API Center, MSFT

Overview Notes:

- Newest service for the API Platform system.
- Azure API Center is now GA.
- API Discovery, Consumption, and Governanace are all managed within the Azure API Center.
- VS Code Extension: Azure API Center. Now GA and enables viewing and registering APIs with Azure API Center. Will auto enable CI-CD automation of Registration.
- Azure API Center can register any type of API: HTTP, gRPC, GraphQL, etc.
- Azure API Admin experience includes a list of registered APIs, drill-down into lifecycle, API type, and Summary descriptions.
- LogiApp Workflows can be set up to alert users via Email when changes happen to registered APIs.
- Metadata can be added to registered APIs via API Center. These metadata can apply to compliance rules, ownership, or other properties as needed for the specific API.
- API Analysis in API Center is focused on API design governance. Various specifications and standards can be checked and alerted. This looks inside the API defiition and flags warning and errors where the JSON does not follow governance rules. Non-compliant APIs will have a Compliance URL made available that can be imported into VS Code so the developer can easily find the compliance errors/warnings and fix them.

## Highly Technical Talk - Hanselman and Toub

Presenters:

- Scott Hanselman, VP Developer Community, MSFT
- Stephen Toub, Partner Software Engineer, .NET Team, MSFT

Humanizer:

- Varied functionality creates outputs that are more human readable.
- Various Profilers are available in Visual Studio.
- Object allocation consumes resources in .NET.
- `+` used as a contactenator is syntactic sugar for te `string.Concat(args [, args])` method.
- `Span` didn't exist multiple years ago, but now that it does, it is time to apply it in newer .NET SDK implementations.
- Humanizer `To.SentanceCase()` means to ensure the 1st character in a sentance is upper-cased.
- Adding a method overload is one way to add or fix issues in OSS contributions.
- "The thing with scale is, if you can do it without allocating anything, you can do it infinitely." - Scott Hanselman
- Ideally, when profiling and optimizing for performance, the developer would have a set of contexts and use cases where the optimizations are impactful. One example is "hot path" evaluations.
- DO: Benchmark your application and evaluate it based on actual usage. While it is possible to deep-dive into the core functionality, it might be better to focus on the business value, and to work with the .NET team(s) to get help addressing the core, low-level optimizations (which might help the ecosystem).
- `RomanNumeralExtensions.FromRoman(string)` is a parsing operation and it should be "pretty close to free".
- RegEx Capture Groups have an additional cost. If all that is needed is a boolean match _do not run capture_.
- Enumerating Arrays is _much faster_ than enumerating a `Dictionary<K, V>`.
- Keyboard tip: `Alt` + `Mouse Drag` across a column of text to edit all items within the drag simultaneously.
- `UTF-8` vs `ASCCI` case-handling: Use character code `` to `AND` with the input to convert between lower- and upper-casing.

## Zero To Hero - Develop Your First App With Local LLMs On Windows

Presenters:

- Craig Loewen, Product Manager on WSL and AI, MSFT
- Alexandre Zollinger Chohfi, Software Developer Engineer, Windows Partners Team, MSFT

Goal: Walk away knowing how to make 2 apps using GitHub, PyTorch, SML, PDFs, ONNX, and RAG...all running locally!

ML Models:

- Programs that use data to make predictions, based on new data.
- More parameters leads to larger models.
- Types of models are better at certain things like "sentiment analysis".
- SLM and LLMs: Language models of varying sizes. GPT-4 is large; Phi-3-mini is small (500x fewer parameters).
- Training vs Fine Tuning: Many models are already trained, and it is up to the Developer to fine-tune the model(s) for a specific implementation.

AI GitHub Issue Labeler:

0. PowerToys repo and VS Code on WSL: Issue Labels are manually created and applied to Issues in GitHub. Labels are not necessarly intuitive.
1. Pick an AI Model and Framework.
2. Install Dependencies and runtimes.
3. Train (fine tune) the Model on custom data.
4. Run the Model.

AI GitHub Issue Build Notes:

- `winget search arg` to list all Packages that are available, filtered by `arg`.
- `winget show arg` displays `arg` Package information including dependencies. In an elevated shell, `winget` will handle Windows Feature installations too!
- Install AI Toolkit Extension for VSCode.
- Click the Fine Tune option and select a Model. Phi-3-mini-4k-instruct was selected for this demo.
- The Data Settings page will appear for tweaking parameters.
- `olive-config.json` is used to configure and fine-tune the SLM.
- Data is grabbed from `dataset-classification.json` (in this case it was downloaded from GitHub). This is static data, which can be used to fine-tune your local model, and is not portable for an LLM cloud deployment.
- Use Python and Flask to quickly generate a website.
- Models must be "loaded" within the RunTime code. This is actual Python code that sets up the model fo ruse.
- Inferencing means adding data to the model locally. Calculating a result processes the Inference input and the SLM will provide a result.

What is ONNX?

- Common format for ML Models.
- Can be exported from PyTorch and Tensor Flow (and others).
- Cross platform (desktop, iot, mobile, cloud).
- Fast and supports DirectML (like Direct3D but for maching learning).
- Supports GPUs, with NPU and CPU support coming soon.

Personal PDF Query Tool:

0. 100% local!
1. Can't send entire PDF to Phi3 (too much data), so utilize RAG and find just enough PDF pages to set the context via RAG instead.
2. SLM will take grounting from RAG. Fine-tuning is used for static data. RAG is used for dynamic data.
3. Vector Empbeddings Model is resulted, and is used for searching, grouping, classification, and recommendations.
4. SLM receives the data, and uses prediction to complete input generation.

> Essentially, all this work creates a "semantic index" that is used to respond to queries by a user.

PDF RAG Query Tool Build Notes:

- Use WinGet to install requirements and their dependencies. Configurations can also be set in WinGet, by supplying a YAML file. This is "machine setup" all with one command!
- Download Models via [HuggingFace](https://huggingface.co), which is a catalog of available models of various sizes and uses. Most HuggingFace index models use ONNX.
- Develop the code to read through your specific input types. Note: HuggingFace has help and starter code for the SLM/LLM you are tuning.

> Leverage models locally without having to understand every detail about how fine tuning and RAG!

Get started by using "AI Toolkit".

Use [OLlama](https://github.com/ollama/ollama) for local testing!

## Windows Subsystem for Linux, Your Enterprise Ready Multitool

Presenters:

- Pierre Boulay, Sr Software Engineer, MSFT
- Craig Loewen, Sr Product Manager, MSFT

Overview:

- Everything in WSL is integrated into the Windows system that it is installed on.
- VSCode runs in Windows, but can target Linux Apps with WSL under the covers.
- Real Linux GUI Apps will run within WLS!

"Get your work done on Linux, even while working in Windows." - Craig Loewen

Latest Improvements:

- AutoMemoryReclaim: Full Linux kernel is running within WSL, so the VM will take Windows memory, over time. When AutoMemoryReclaim is enabled, it will trim the Linux cache, making the memory available to Windows again. All of the Cache can be dropped if necessary.
- Storage: Dynamic (growable) VHD files are used to store the Linx instance, which means VHD file size will grow, and deletion is not reclaimed back to Windows. SparseVhd enables reclaiming that space. `wsl --manage --set-sparse` will force instance reclaimation. Otherwise, VHD compaction operations are necessary.
- Networking: DnsTunneling, MirroedNetworking, and Hyper-V Firewall support.
- MS Edge is available from within WSL. Edge _is a Linux app_! This supports EntraID authentication too!

Details on DNS in WSL and Latest Improvements:

- How it used to work: `/etc/resolv.conf` is standard resolver. An internal resolver exists between Windows and WSL, therefore DNS record resolution can be hindered between WSL and the internal resolver, or the resolver and the Windows firewall or network interface. WSL traffic is seen as a network packet within Windows.
- DNS via NAT is WSL: This is usually more reliable, with the drawback of losing the Windows DNS configuration.
- DNS Tunneling in WSL: Set a loopback ip e.g. `127.0.0.42` and bind it to the `Guest Network Service` for handling DNS requests via a Socket to `wslservice.exe` (on the Windows side) where all the DNS rules and configuration is applied, and external DNS is readily available. The Socket has the benefit of not being inspected by Firewall rules. This is enabled by default in WSL (latest) on Windows 11.

Details of NAT Networking in WSL and Latest Improvments:

- All processes must use the `ethn` interface, which talks with `Host Networking` via the ineternal network, then the Windows Networking decides which of its interfaces the packet will traverse.
- Port binding within WSL is _not reflected in the Windows port_ unless the port is manually mapped.
- Mirrored Networking: Creates mirrored Windows network interfaces for WSL to talk to directly. Port bindings _are translated to the Windows interface(s)_.

Security in WSL:

- Hyper-V Firewall: Best solution to control network traffic traversals to and from WSL.
- Loopback: Between WSL process and Windows process.
- Outbound: WSL to elsewhere.
- Inbound: Elsewhere to WSL.
- `.wslconfig` is used to configure Hyper-V Firewall to apply Windows rules to WSL.
- Use `Set-NetFirewallHyperVVMSetting` psh to create or change rules.
- Latest WSL on Windows 11 enables utilization of Hyper-V Firewall, secure by default, out of the box!

Zero Trust:

- MSFT Defender Endpoint plugin for WSL: Get alerts _inside WSL_!
- MSFT Entra ID: Preview for this allows connecting to application seemlessly, if already authenticated!
- MSFT Intune: Custom deployment scripting is available.

Plugin Support for WSL:

- Windows > WSL Virtual Machine > One or more Linux distro installations.
- `wslservice.exe` talks wto `Plugin`, which is a proxy for the WSL Virtual Machine, and any distos within it.
- `WslPluging` interface requires local Administator access to make changes, and runs in Windows (not WSL).
- There is an option to create custom Plug-ins for WSL!

Coming Soon:

- WSL Settings App: Graphical settings!
- Dev Home: Manage WSL Distros (coming soon, currently in 'canary' mode)!
- VS Code AI Toolkit: Built-on and uses WSL. Fine-tune SMLs directly on your device.
- Windows Package Manager: aka `winget` now supports installing WSL locally, or in the Enterprise.

## Whats New In C Sharp 13

Presenters:

- Mads Torgersen, Principal Architect, MSFT
- Dustin Campbell, Principal Software Engineer, MSFT

Starter Info:

- Comes out with .NET 9.
- Focusing on 3 specific features: Extension Types, Auto Props customization, and Collection Expressions with auto-typing.
- Preview implementations are available in the compiler bits, just by using In-Preview bits.
- New documentation articles are released as new features become available [link placeholder](csharp whats-new csharp-13) #####
- [dotnet/csharplang](https://github.com/dotnet/csharplang): This is the design-level repo.

General Notes:

- Collection Expression: `[]` converts to any type without specifying, other than hints like `m` for decimal, etc.
- Params array: Now supports `params IEnumerable<T>`. Remember, IEnumerable has its own costs.
- ReadOnlySpan(params ...) overload: This is based on non-allocation `Span`.
- AutoProps was added in C Sharp 3: There is a cost (the cliff) when moving from autoprops to full props when custom code is necessary. A new keyword 'field' will be added to enable using a lambda to do a simple task like `.Trim()` on a string prop. _Note_: This is not fully baked yet! _Note_: This is a breaking change, since assigning `field` to a keyword could impact existing code! _However_ the `@` identifier can be used to _disambiguate_ your custom `field`
- "Extension Types": Use `implicit extension name for type` in place of `class` declaration to transform the type definition into an Extension Method. There is also a Static Extension Method.
- "Explicit Extension Member": A lightweight type. Used within an Extension Type that will (in the future) be available to enforce the type explicitly. Basically, it scopes _down_ the type assumption to the specified _instances_. The current C Sharp 12 work-around is to enforce the type with `EnumerateArray<T>`.

Question of the day: "What other types of Types can be extended by Extensions?" -Fred, on the C Sharp team.

## Level Up With DevBox

Presenter: Scott Hanselman, VP Developer Community, MSFT, "Programmer"

General Notes:

- Github Copilot at CLI: Prefix query with `??`.
- [GIthub Copilot for CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli/about-github-copilot-in-the-cli)

Kayla Cinnamon - Windows Team MSFT

- Single-click arrange windows.
- Applies to multiple screens or projects layouts. DevProject!
- DevHome: Dashboard of projects, Machine Configuration, Environments, Windows Customization, and Utilities.
- DevHome Machine Configuration can export a configuration file (YAML) to replicate to other developer machines/images, using `OneGet` (uses DSC - Desired State Configuration).
- DevHome can detect configuration files for importing, editing, and running. Dependencies are listed and included.

Maddie Montaquila Sr Prgram Manager, .NET Team

- PhoneLink demo: Mirroring screen, app casting.
- Visor: Screen Mirror from phone to remote screen.
- ScreenSnip tool: `Win` + `Shift` + `S`. Now has AI to OCR.
- Edit `hosts.` file to create aliases (I'd forgotten about this).
- Color Picker: `Win` + `Shift` + `C` to launch it. Displays HEX, RGB, and HSL codes.

Vickie Harp, Principal Group Product Manager

- PowerToys can be used to browse Control Panel, the Registry, and more, directly from the PowerToys `Run` tool.
- Polyglot Notebooks: Like Jupyter Notebooks, but allows `C#`, PowerShell, Python, etc.
- `sudo` has been added to Windows.
- FileLockSmith: SHows what process is holding a file handle.
- PowerToys Advanced Paste: AI-assisted paste. Will paste-as to types like JSON, Markdown, and other types including `paste audio as text`. _These features are running LOCALLY_ not in the cloud.

Mike Grie, Sr. Engineer, Windows Terminal/Command Line Experience

- Global Hotkey configuration via JSON to bring Terminal to the front/focused application.
- Shell Integration: Terminal Copilot is aware of the Terminal History.
- Scroll To Mark: Navigate between prompts within the Terminal, through the command history.
- Terminal can provide a list of previous actions to quickly find items in history.
- Snippets: Available within a command menu, directly at the command line -- Snippets for Terminal!
- Ctrl + Shift + N: Highlights hyperlinks in Terminal output.

## AI Safety and Security Fundamentals

Presenter: Neil Coles, AI Safety and Security Empowerment Lead, MSFT

General Notes:

- Look for security risks earlier in the development lifecycle - prevent the security risk from the start.
- AI Red Teaming is used to test security of AI-enabled apps and services.
- Developer's goals should include making Red Teams' job difficult!
- AI is, after all, software. Many of the common/traditional weaknesses are possible. The infrastructure can bring the AI software/service down.
- AI can be attacked through the language they are consuming. AI is non-deterministic, so slight changes in input can have a dramatically different outcome.
- Apply multiple mitigations and hope that the weaknesses don't "line up" between them, and get through to the system. Guiding inputs through the mitigation layers will subvert the mitigations and allow the attack anyway.
- Intrinsic System Risks: System compromise (Worms), overreliance aka inappropriate reliance (don't believe the AI unless you "should" believe it), widening (get outside the designed use cases).
- Input/Output Risks: Exclusory Interpretation (system fails to interpret an aspect of the normal human experience e.g. US English vs UK English vs AUS English), Content Production & Dissemination (content that has a harmful effect when shared e.g. propaganda, etc), Content exposure (generated content causes harm to the user), knowledge recovery (borrowed expertice, e.g. instructions on how to make bombs).
- Human impersonation (deep fakes of all sorts), Ability amplification (spearfishing email generation as a service, hyperscale cyber incidents driven by an LLM).

- --

Proactice to Reactive actions:

Prevention:

- Security education
- Security requrieents
- Secure design
- IDE Static analysis

- --

Detect and Mitigate- Secure pipelines

- Static Analysis
- Secure pipelines

- --

Test/QA

- Dynamic Analysis/Fuzzing
- Offensive Operations

- --

Test/QA

- Bug Bounty
- Security Incidents

- --

As you get farther down the above list, the potential costs go up rapidly.

Safety and Security are not distinct.

Use Threat Model designs to better understand areas where threat risks exist.

- Identify trusted and untrusted inputs and data, such as user inputs, or some extreme content from the LLM.
- Other untrusted inputs could be 3rd party websites with images, audio, text, or files. The AI could interpret various encodings and code as instructions.

Jailbreaking:

- Get the system to do something regardless of the rules set for it.
- A fancy way to 'code' social engineering.
- Dealing with humans: Vetting, training, monitoring, checks & balances, and build trust over time.
- Dealing with AI/Copilot: Test through adversarial methods, adjust meta-prompts to tune behavior, monitor, include multiple AI systems and/or humans managing them (metacognition).

XPIA: Cross-Prompt Injection Attacks

- Embedding malicious prompts into a web page.
- AI uses the "tainted web page".
- AI performs a transaction as instructed.
- LLMs confuse actual inputs with tainted inputs that _look like instructions_.
- Mitigate by delimiting data, marking data, and encoding data.

Advice:

- Do security fundametals/training.
- Look fo rai risks early on.
- Use safety mitigation builtin in to oplaform you are using.
- Plan enough time to test ai enabled applications.

## Enterprise Class NGINX Plus Without Operational Toil

Dona interviewed Brian Ehlert, Director, Product Management, F5 NGINX.

General Notes:

- NGINX is _more_ than just a web server: Cache, reverse proxy, streaming server, etc.
- Clustering and state sharing: Client connection state is shared within the cluster with features like rate limiting.
- NGINX as a Service, 1st class service on Azure.
- NGINX+ unlock developer capabilities as a managed service, in L4 and L7 (which other services do not provide).
- Header and Body manipulation are possible, as well as authentication and session handling.
- More about [NGINX as a service on Azure](aka.ms/Build24FP/F5).

## Scott and Mark Learn AI

Presenters:

- Scott Hanselman, VP Developer Community, MSFT, "Programmer"
- Mark Russinovich, CTO and Technical Fellow for Microsoft Azure

Live build an AI ChatBot using C#, .NET MAUI, Semantic Kernel, Github Chat (custom box), to clean Scott's desktop:

- An initial AI Copilot doesn't have any guardrails - "poor alignment" and the model starts out as a blank slate.
- MetaPrompts should not be considered secrets - they don't have 'secret' instructions, and shouldn't have anything that might be leaked.
- Red Teaming out own Chat Bots: Evaluate the risk first. Safeguards should be put in place to minimize the risk.
- Fine-tuming might be required to get the Bot to do things like _count files in a directory_.
- Semantic Kernel is the platform that will provide deterministic-like actions.
- The Chat Bot will need the capability to do things like read files. Do this by adding Kernel Functions with `[KernelFunction]` attribute. This declares "arms and legs", meaning give it the ability to do things like count files in a directory. These `[KernelFunctions]` attributes add to the list of "things I can do".
- The Cloud-based AI does not know what the functions in the Application contain, it only knows (through Semantic Kernel) the calls it can make.
- .NET Aspire Traces can drill-in to the inter-process communications to see the prompts, responses, etc.
- Endpoints are set up in the App configure container. Mark and Scott set this up to use 2 specific AI Chat Completions, to run on the MPUs on the local machine.
- "Summarizing text files is something that SMLs can do really well".
- AI Models are non-deterministric, matching tokens that it saw while it was in training. Probabilistically, the result is more likely to be closer to its training, rather than veering from the deterministic path.
- Deterministric Functionality, through Semantic Kernel, allows the AI Model to handle the actual data that the App has information about, or direct access to.
- Models will ask for concent before doing destructive actions.
- UX, ethical, and philosophic questions must be considered and dealt with, because the AI Model _will not have these capabilities_.

## .NET Aspire Dev On Any OS with VS Family

Presenters:

- Wendy Breiding, Sr. Manager, Product Management, MSFT
- Brady Gaster, Principal Product Manager, MSFT

What does .NET Aspire mean for .NET cloud native? Simplify deployment and onboarding!

Requirements to get started with .NET Aspire:

- .NET SDK
- .NET Aspire workload
- Docket desktop
- VS Code/VS
- C# Dev Kit
- Azure Developer Clie (azd) Extension
- Azure Resources Extensions

_Note_: New .gitignore using `dotnet new gitignore`

New: .NET Scaffold!

- Can select a category e.g. 'Aspire'
- Sub categories include things like 'Redis'
- Select the App Host project (points to a CSProj file).
- Dials-in components and updates the target project(s).
- Will scaffold-in the selected sub-category.
- This is PRE-RELEASE and is in evaluation - MSFT wants feedback on this.

C# Dev Kit:

- Open the Command Palette and select create new project for .NET Aspire.
- New to C# DevKit: Add NuGet Packages!
- Right-click a Project and use the Command Palette to Search for the package to add.
- CSProj file is updated, etc.
- Add the commands to the `builder` functions in `Program.cs` to add the NuGet package (e.g. Redis).
- HotReload (coming? now available?)!
- Add some tests by adding a New Project :arrow_right: .NET Aspire Test Project.
- References from test Project to the AppHost Project(s) will be necessary.
- Sample Tests are included, they just need to be commented out! :tada:
- Fast and easy setup :arrow_right: run!
- `azd` commands are available in the Command Palette!

Aspire, Visual Studio, and Azure can work together to spin-up, develop, test, publish, and monitor apps!

Dashboard Notes:

- The Trace view is live, so while the app is running, the Trace entries will be loading and listing very rapidly.
- Drilling-in to a node displays inter-process communications with just a click.

Publishing in Visual Studio:

- There is a SINGLE Publish Button presented on the Aspire project.
- Executing the Publish will actually Publish all of the publishable assets via `azd` to push them into Azure!

## Demystify Cloud-Native Development with .NET Aspire

Presenters:

- Damian Edwards, Principal Architect, Microsoft
- David Fowler, Distinguished Engineer, Microsoft

.NET Aspire is now GA as of a couple days ago! Was previewed in November.

Scenario:

- New team member, trying to get ramped up, just cloned a repo.
- Starting the project directly from VS/VSCode usually won't work because Startup Config is stored in VS User configuration.
- There are usually secrets, especially when DB connections are required, etc. Multiple projects in a solution might need their own secrets!
- Is the DB that is necessary actually installed and running?
- There might be other issues with configuration, secrets, authentication, etc that might make project onboarding very difficult.

.NET Aspire Aspires to Solve This Problem:

- Create a new Project based on .NET Aspire template, adding it to the existing Solution.
- `DistributedApplication.Createbuilder(args)` in Program.cs is the entry point.
- Add Project References to the other Projects in the Solutions.
- Add Extensions and other dependencies for things like Databases etc.
- Add resources within the Application model e.g. `builder.Add*` commands in Program.cs.
- `.WithReference(target)` tells the DistributedApplication builder to tie-in the dependent projects.
- `<Projects.ProjectName>` is a special Type that .NET Aspire uses to generate classes representing the referenced Projects.

Aspire Dashboard:

- Aspire is Developer First.
- The Dashboard is automatic and displays the layout and information about the Solution: Endpoints, Logfiles
- Traces and Structured Logs.
- Metrics tab: (explained later).
- Defines the types of containers and the endpoints and environment variables.
- Is Open Source!
- Is available as a stand-alone Container!
- Data in the Dashboard is stored in memory, not long-lived production-data ready.
- This is a great way to verify that logging and telemetry are working within 1 minute of build + run an app, without having to build your own queries and report pages or using a 3rd party thing.

Aspire "just codifies the patterns that your probably already using". - Damian

Add a Service Defaults Project

- This is a .NET Aspire project type.
- Contains a single file, `Extensions.cs`.
- This is used to enable basic defaults that are assumed to be the correct things to enable for the existing app.
- Configure Telementry, add Health Checks, enable restarts (ResiliencyHandler).
- The goal is to get the developer started on a well designed, robust app architecture.
- Back in the .NET Aspire Program.cs, add the defaults that were defined in this `Service Defaults` project.

After the Service Defaults Project references are added, then the Structured Logs, and Distrubuted Tracing data will appear in the Dashboard.

_Note_: .NET Aspire performs these actions automatically, and the demo is just walking through what .NET Aspire does for demonstration purposes.

_Note_: Drag-and-drop Project files on other Project files in Visual Studio _adds a Reference to the dragged Project to the dropped Project_!!!

Aspire Components:

- Get more data from things that are talking to cache and database services.
- Add health checks so that if cache goes down, certain actions can be triggered.
- Add `.NET Aspire Package` using NuGet.
- There are a bunch of 'glue packages' and add Health Checks, Telemetry, Metrics, and Configuration.
- Packages are meant to 'glue' the things together into a single package, but does _not_ bind your project to Aspire in any way. Essentially, Aspire just exposes the APIs so that the 'glue packages' can provide the information and configuration.
- `Enrich` prefix syntax is used to simplify DB configuration in the DI Container, too!

David Fowler Demos Stuff:

- Extend the application model by "just writing more code".
- Containers, executables, and packages are just treated as resources by Aspire as part of an overall runtime state.
- ONce the code is written (or NuGet package is added) then add it to the `builder` in the base project's `Program.cs`.
- Open Telemetry makes it possible to easily see into your apps, including endpoints, for direct access to the endpoints _and_ to see what is normally reserved for seeing is a Production environment (this is _shifting left_).
- Aspire will help deploy an Azure resource (example was Azure Service Bus, which cannot be deployed locally) so you don't have to.

These notes cannot possibly describe _just how good the presentation and demoes were_. Find the recorded version in the future and _watch it_.

## Build and Deploy to Azure with GitHub

Speakers:

- Jessica Deen, Staff Developer Advocate, GitHub
- Mandy Whaley, Partner Director, Azure Dev Tools, MSFT

They will build a RAG (Retreival Augmented Generation) app live with demos.

- Stay in the developer inner loop by working with Visual Studio/VSCode and have access to Azure Dev features.
- Supports Windows, Linux, and macOS...by running CodeSpaces instead of VSCode locally.

Start in a Github Repo:

1. Navigate to Code button.
2. Click on the CodeSpaces tab.
3. Create a CodeSpace with the '+' sign or the '...' to configure a DevContainer.
4. Choose to open VSCode in the browser, or allow opening in local VS Code.

Copilot Chat is available:

- In CodeSpaces, or by adding as an Extension to VSCode, Visual Studio.
- Asking Copilot a question, prefixed with `@codespaces`, will produce results targeted to the entire solution in this CodeSpace.
- Copilot has the usual features such as `/doc`, `/fix`, `/explain`, etc.

Building a Project - how to take working code in CodeSpaces, up and running in Azure?

- Azure Developer CLI - AZD
- `azd up`: Provision and deploy in one step (well, respond to some questions to configure the deployment).
- GitHub Copilot for Azure: Help with using Azure and managing Azure services configuration (currently in Preview).

AZD Pipeline Config:

- Helps with configuring Github Action Workflow including secrets and variables management.
- Edits `azure-dev.yml` file, which templates the project for use with Azure services.
- Ask Copilot questions like how to deoloy. Prefix the question with `@azure` to get the proper context.

Deploy Using Github Actions:

- "We are now in the Managed Identity age".
- GH Actions is the number 1 tool for deploying and publishing projects.
- Customized Actions are available (of course), as well as pre-built Actions from a GH Action Marketplace.
- GH Actions for Azure: Owned by Azure Service Teams (therefore are guaranteed to work and supportable).

Automating Workflows:

- Build, Test, and Deploy.
- Also: Evaluate, meaning "Prompt Flow Evaluation". A build artifact has the result from the workflow action, which can be published because _they are just markdown files_!

Operate: Once build and publish is completed with established pipelines, consider "day 100":

- Code Scanning: Uses CodeQL. Address problems early in the workflow. Added generative AI to provide "editable suggestions" to fix issues via Pull Requests.
- Secrets Scanning: AI-powered scanning helps find 1000's of types of keys and secrets. Will help to prevent pushing secrets to the repo to begin with! Just "click and enable", then update config from there. GitHub will _reject_ the push and include the path, codeline, and the commit that was rejected.
- Dependabot Alerts: (They didn't discuss this during the demo).

### Additional Information Based on Hands-On Experience

1. Open Codespaces in the repo to be deployed (same as above).
2. Install Azure CLI using a new Codespaces Terminal: `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`
3. Login using `az login --use-device-code`. Skipping the device code argument failed for me on multiple attampts.
4. ...Ran into Azure issues that I have to resolve before continuing.

## Building Custom Copilots with Copilot Studio

[Copilot Studio](https://www.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-studio) has solutions for every industry.

- Internal, external.
- Security ops, customer service, sales, development, knowledge workers, data, and IT Pros.
- Varying use cases, reducing time to solve issues and complete tasks, and increasing development speed.

Building a Custom Copilot is easy:

- Build and test together with Copilot. Users at all levels can build Copilots.
- Design personalized, responsive interactions.
- Boost conversations through dynamic and real-time Copilot responses.
- Complex queries are handled using LLMs.
- Continuous self-learning and improvement: OOB analytics and optimizations. Copilots can be _taught_ how to handle specific situations.

Process to Build a Copilot:

- Stand up Copilot Studio SaaS.
- Connect knowledge base for generative answers. Create rule-based topics. Integrate plugins and data connectors. Exptend with Azure AI Studio.
- Publish Copilot to Teams, websites, apps, solcial media channels, etc.
- Monitor and manage the application and custom Copilot through its lifecycle.

Copilot Investment Themes:

- Rapid time to value.
- Maker advancements.
- Security and analytics.

"Build & Publish, Analyze & Improve", rinse and repeat.

Using the "Creation Experience":

1. Describe your custom Copilot in Copilot Studio using the Copilot Chat interface.
2. Describe what to include, using plain english, the focus of your custom Copilot.
3. Provide any Tips and respond to other prompts from Copilot Studio Copilot chat.
4. Describe the topics and tasks the copilot should NOT address.
5. Click Create!
6. Test and tweak your custom Copilot.
7. Publish your customer Copilot.

_Note_: It is possible to fill out a Form and configure your custom Copilot that way, instead of using the Copilot Chat interface.

After configuration, your custom Copilot appears as a Copilot Chat interface that has the configuration, description, and other items like knowledge sources, etc. The Chat interface should be used to test the custom Copilot at this point. Adjustments can be made from this view, as needed.

Extending Your Custom Copilot with Additional Knowledge and Actions:

- Instruct Copilot how to format information such as Dates and Currency.
- Public Websites can be added or adjusted (Knowledge Sources). DataVerse is already available, and Azure will have a Knowledge Source soon).
- Knowledge Sources are used to identify data properties that the custom Copilot will have access to. This enables search over structured data via the Copilot Chat interface.
- Knowledge Source utilization is _case insensitive_.
- Extend Actions in Copilot Studio to add a fluid experience to provide effecient results for users.
- Think of an Action as an API wrapped in metadata.
- Multiple Intents can be included in a prompt and Generative AI will figure out what Action(s) are needed to find a useful response and display it _without asking follow-on questions_.
- Authentication pass-through is allowed (from Teams or other auth mechanisms like passwords).

Fully Generated to Fully Authored processing and respponses are possible using a custom Copilot:

- Enables Copilot developer to fully control the inputs and outputs.
- A combination of full control as well as AI-backed responses is possible through Topic Details configuration.
- This will enable Copilot to identify missing _required_ information and prompt the user for it.
- Natural language terms like "actually, it was the day before yesterday", interrupting the Copilot response _and_ providing a human-like input that Copilot understand and can transform into a calendar date.

Note: There are additional settings that can be applied to Topic Details at anytime during development and testing of the custom Copilot. These settings help to define how many times to reprompt, and other aspects.

Adding Files As Knowledge Sources:

- Files can include text or visual information such as charts and graphs.
- Various file formats are supported (PDF was demonstrated).

Other features overview:

- Copilot Analytics: Enabled drilling into data and generate charts and statistics on the input data.
- Security Granular Controls: Enable turning on-and-off various aspects of security, topics, and authentication.
- Authentication: Can be set to User Auth, or Copilot Author Auth.
- Sharepoint Grounded Responses: Only provides responses that are within the user's existing permissions.

## Keynote - Wednesday

"Next Generation AI For Developers With The Microsoft Cloud"

Primary Speaker: Scott Guthrie

- Yesterday: What's new with the Copilot Stack.
- Today: Delve into the Copilot Stack and how it works.
- Popular trio of dev tools: VS, GitHub, and Copilot Studio (released in 2023).
- GitHub uses an LLM on the back end, and is used by millions of developers, globally, daily.
- Demo: Copilot Workspace: Advancements to Copilot Chat, including suggested fixes, documenting code, and creating pull requests for you.
- Over 50k licenses of Copilot for Business, currently.
- .NET Aspire is now [GA](aka.ms/AspireGA)
- Copilot for Azure enables Natural Language input within VS and VSCode. User is always required to actually take the actions that GitHub Copilot for Azure suggests. Right-click manu enables shortcuts to Azure Portal for specific views and actions!

Charles Lammanna:

- Copilot Studio can operate asynchronously.
- Copilot Studio can orchestrate operations, end-to-end.
- Copilot Studio can be used to design a Copilot to digest a PDF, analyze it, and return results based on a prompt. This saves the user from having to enter specific information one at a time. In the Demo Charles ran, he showed the Copilot asking for and using a Phone Bill to compare to the Fabrikam Carrier service to see what savings his ficticious customer might see by becoming a new customer. That 2 chat exchanges, 2 clicks to upload a file, and a result on-screen!
- Various Connectors to on-prem and Cloud based functions.
- Topics: Design triggers that a user might input to determine response(s) through specific workflows. The problem this attempts to solve is the 20% part of the 80/20 development problem.
- "You want your Copilot to run asynchronously and execute flows in the background": Triggers. These start execution of the Copilot, triggered by the data that is input _by the Trigger itself_ for grounding the Copilot responses. Various Trigger Steps define the available responses given specific scenarios.
- Over 30k orgs are already using Copilot Studio.

Scott Guthrie on Azure AI:

- Customer adoption is accellerating.

Eric Boyd:

- Azure AI Studio: Build generative AI solutions for Azure.
- "Foundation Models": Azure AI, Azure ML, Responsible AI Tooling, and Azure AI Studio.
- [Azure AI](https://AI.Azure.com)
- Azure OpenAI Service: Enterprise grade AI service.
- See [GPT-4o](aka.ms/GPT-4o) which backs Azure AI services.
- Azure OpenAI Batch Service: Reduced price announced.
- Frontier and Open-source models are available via Azure AI services. Phi, Meta, Mistral, Cohere, Hugging Face, etc. See the [Model Catalog](aka.ms/ModelCatalog), [Phi-3](aka.ms/Phi3) and [Phi-3-v for Vision](https://news.microsoft.com/source/features/ai/the-phi-3-small-language-models-with-big-potential/).
- Azure AI Search supports all of OpenAI's GPT instances.
- Azure AI Studio is now GA.

Seth Juarez:

- Demo using Copilot Studio to configure "Trade-in purchased product" on the demo Fabrikam website.
- Using internal data without exposing it: Goal is to do it safely, reliably, and in an observable way.
- To implement using internal data safely follow this paradigm: Discover, Delivery safely and reliably.
- Promptly: A way to move a custom prompt to the development IDE. It uses placeholders for where the values will be placed within the prompt response. This moves the Copilot Studio "Playground" into the development IDE.
- Customer, Policy, Response: The 3-liner code that runs behind Copilot that is part of the codebase, without divulging customer data.
- Use Github Actions to _Deliver_ safely and in a reliable, observable way (see next bullet).
- Groundedness test: How well does the data fetch stay without leaving the bounds of the prompting.
- Trace: Adds Observability to the developed model. This is available _in production_!

Sarah Bird (Chief Prod Officer at Responsible AI):

- AI Principles are the start of the story of [Responsible AI](https://www.microsoft.com/en-us/ai/principles-and-approach).
- Safety and Security are baked into the stack.
- Safety system sits between User Input, AI Models, Monitoring, and the response mechanism.
- Filters can help block direct and indirect jailbreak attacks.
- Create a Check, add a Flow, select data-set to evaluate, adjust sampling, and harmful content and jailbreak.
- Microsoft Defender for Cloud is integrated into Azure AI, and has been built-up to understand jailbreak and content policy violations.
- Custom Categories: Create custom filters for unique needs of your Org and/or Application/Service.
- HiddenLayer Announcement: Company created "Model Scanner" and MSFT is using that to help secure AI systems. This enables automated alerts about data leaks and other policy violations.

Eric Boyd:

- Epic is featured.
- AI generated draft messages in email. Review and accept/edit before sending is default behavior.
- Reduces time spent on messages by 30 seconds and has been reported to reduce physician burnout by simplifying the message/response process.
- Slicer-Dicer: Helps phsyicians understand conditions, remedies, care, etc. In effect, enables natural language evaluation of real patient data so the Physician to gain insight quickly, and remain productive.

Scott Guthrie:

- MSFT Intelligent Data Platform.

Arun Ulag: Corp VP Azure Data, MSFT

- Portfolio of products across AI stack, in Azure.
- DB's, Analytics, AI, Governance.
- Note: Chat GPT is powered by Cosmos DB (that's on Azure).
- Copilot Self Help for Azure SQL DB
- " natural laguage to T-SQL
- Vector Search for Cosmos DB, NoSQL Search using AI. This targets building RAG Models.
- PostGresQL: Azure AI Extension now GA. In-DB Embeddings in Azure DB for PG now in Preview.
- Microsoft Fabric was previewed in 2023, and in November 2023 became GA.
- Fabric is a SaaS platform for AI. Unified storage, comput, experience, governance, and business model.
- 11k Orgs using MSFT Fabric since GA in November.
- Real-Time Intelligence on streaming data now available in MSFT Fabric.
- At least 20 Orgs are developing on top of Azure Fabric, including Neo4J, LSEG, and others.
- MSFT Fabric Workload Development Kit: Monetize, grow business on top of MSFT Fabric.
- OneLake: A Data Lake service by MSFT.
- OneLake uses Apache and Open Data Lake under the hood.
- Azure Databricks and Microsoft Fabric have the same data format using OneLake.
- GA of Vector Search in Azure Databricks. Databricks Catalog Tables coming soon.
- Data stays in sync as services sit on top of OneLake.
- Announcement: Snowflake now a part of the MSFT ecosystem, due out by end of 2024.
- Announcement: Apache Iceberg support in OneLake.
- MSFT is contributing to the Apache X-Lake project now.

Christian Klienerman, EVP of Product, Snowflake

- Chat about how MSFT and Snowflake get along and things are going well.

Back to Scott Guthrie:

- Azure "the world's AI supercomputer". More than 60 Azure Regions around the world.
- Committed to, and on-track to reach 100% of energy from zero-carbon sources by 2025.
- MS Azure end-to-end systems optimization.
- AI Accelerators in Azure: NVidia, AMD, and MSFT.
- MS Cloud for Industry: Providing Copilot and AI solutions, specific for many industries.
- Azure Marketplace: Billions in revenue per year now.
- Safety and Security: Devs need to integrate these into _every part of the dev lifecycle_.

Julie Liuson President, Developer Division, MSFT and John Lambert corp VP and Security Fellow on MSFT Intelligence:

- Secure by design, Secure by default, and Secure operations.
- Protect ID's and secrets and engineering systems.
- [SFI](aka.ms/securefutureinitiative): Secure Future Initiative.
- Security is a team sport, requiring a culture change.
- Orgs face threat actors. MSFT tracks more than 300 of these entities.
- Logging in is easier than hacking in, so there is incentive to focus on passwords and user accounts.
- Midnight Blizzard: Russian threat actor group. Target government agencies and services, as well as IT globally.
- Traversing the graph of possible security weaknesses is through seeking credentials.
- Github Advanced Security has "Secret Scanning" to find secrets in code.
- Problem is, secrets are just text/strings. Rotating passwords helps mitigate vulnerabilities.
- Rotating Tokens (secrets) is another way to avoid the risks briefly, and must be automated else people just will not do it themselves.
- Better solution is to _not use passwords and tokens_ by default. If the tool uses managed identities, that can eliminate the use of secrets that could get exposed.
- Managed Identities is more complex, so will be slow to import and start using.
- Supply Chain Attacks: Provides an "in" to targeted orgs through their products. The SolarWinds hack was the key example.
- Removing old systems and applications reduces exposure to threat actors, who do not care whether something is up to date, only that it provides a path to gain entry into your systems.
- Lifecycle management is necessary to protect dev and deploy pipelines.
- "XZ Utils" backdoor: Linux data compression library, used by SSH etc. Performance testing prior to publication caught the backdoor. See something? Say something! This will help protect the codebase, and therefore the systems.
- Dependabot: Generates PR and raises alerts. Can be helpful to find and mitigate some security risks.
- Embrace security training. Embrace curiosity, to help find security threats.
- Raise the security posture through customers, partners, and MSFT collaborations and awareness.

Scott Guthrie:

- Recapped keynote key points.
- "It's never been a better time to be a developer."

## Extend Microsoft Copilot Using Copilot Studio

Presenters:

- Mike Bassani, Parner, Product Management, MSFT
- Jeff Derstadt, Eng'g Director Copilot Studio, MSFT

Copilot for MSFT 365 is 'the keystone service' now but Copilot Studio is key (Mike):

- Everything is stored in the MSFT Graph.
- Copilot Studio: The home for extensibility of Copilot.

Copilot Extensions (Mike):

- Wrap around Copilot.
- Operate on knowledge and actions.
- "General knowledge" is not enough to address an org's customer concerns, issues.
- "Enterprise knowledge" is about the data, apps, and M365 Graph knowledge.
- Together, General and Enterprise knowledge inform an Org's AI strategy, and enable Copilot for business.
- Connectors: Send-Response messages for hooking into applications.
- Plug-ins: Append to the connectors to enable workflows and automation.
- Your Copilots: Enable creating your own Copilot using Connectors and Plug-ins.

What's instide a Copilot Extension (Jeff)?

- JSON.
- Can be authored by hand, or generated.
- ID, Name, description: Identify the extension.
- What can it do? Capabilities collection.
- What API or Functions does it have? Actions collection. Think of it like Swagger for Web APIs. "api_description" is what Copilot uses to help make decisions.
- Custom instructions: Instructions string.
- Conversation starters: conversation_starters collection. Help inspire users to provide prompts.
- Copilot Studio is a SaaS. No other services to manage.

Your Copilot, Your Way (Mike):

- What makes the most sense for you/your organization?

Demo Notes:

- Create a prompt by adding a Data Source.
- Provide list of what is needed by adding to the Prompt box.
- Prompt generation will look to resources like "Dataverse" to figure out what queries need to run for training the model.
- Resulting information can be validated by looking at the actual data stored in Power Platform.
- Model (GPT version, etc) and Temperature (predictability) can be selected and adjusted.
- Plugins in Copilot for MS 365 can be Connected and toggled on/off. This includes _custom Copilots_!
- Can be debugged to see what plugin was called by Copilot etc, using "Developer Mode" with prompt `-developer on`.

"Copilot Studio is the home of Copilot Extensibility"

Publishing and Governance, behind the scenes (Jeff):

- Extensions can be published with a single click. Metadata is sent to MS Teams Catalog, then Copilot can find the Extension in the Teams App Catalog.
- Discovery Service caches info, in a multi-tenant view, that lists which Extensions are available by which users.
- A custom Cache "poking" algorithm is used to update the Discovery Service Cache.
- Developers have access to source code, Admins have access to Extensions, Users need access to resources used by the Extension: This is the mix of security concepts in-play with Copilot Extensions.
- Extensions live in an Environment, such as Dev, Test, and Prod.
- Power Platform enables individual permissions lists on a per-Extension basis.
- There are also permissions considerations for Organizations and 3rd Party Services i.e. Docusign, or Azure.

Why Certify Connectors and Plugins? (Mike):

- Expand the reach of your API to users of MSFT Power Platform & Copilots.
- Low-friction options for users to interact with service.
- Ensure success and reliablility before the connecot or plugin goes public.
- This is similar to needing a Developer Certificate to validate the software and the code.

The REST API (coming soon) (Mike):

- Add a REST API Action.
- JSON File is created with a drag-and-drop.
- Export the solution out of Copilot Studio into MSFT Copilot.
- Immediately available in MSFT Copilot!

AI Strategy is anchored in Data Strategy.

No-code, Low-code, or dev code - all are supported.

## Maximize Joy Minimize Toil With Greater Dev Experiences

Presenters:

- Amanda Silver, MSFT
- Shayne Boyer, MSFT
- John Lam, MSFT
- Mark Weitzel, MSFT

Goals:

- Focus on the code that _only you_ can write.
- Allow Copilot to write everything else.

Shayne Boyer demo:

- .NET Aspire templates starter solutions to common project starters.
- Using a more declaritive code style (`.WithReference` et al) to develop an application.
- Use Github Copilot to explain what the template code is and does.
- Copilot Chat keywords `/doc`, `/fix`, `/explain`, etc are helpful.
- Use `@Azure` in Copilot Chat to specify Copilot responses toward an Azure context.

Announcement: .NET Aspire General Availability [GA announcement on .NET Blog](https://devblogs.microsoft.com/dotnet/dotnet-aspire-general-availability/)

Building Intelligent Apps

- If your App already has an API, you're ready to go!
- Consider use-cases: Summarization, Q&A, Data-driven decisions, Personalization, and Automation.
- Natural Language _is_ the new user interface.

Announcement: AI Toolkit for VS Code

- Deploy intelligent APps.
- Integrate small and large language models.
- Deploy to Azure AI Studio or other platforms using container images.
- Windows: Now, MacOS: Soon.

John Lam Demo: Building Intelligent Apps

- Phi-based SLMs can be used on mobile devices or low-powered PC.
- Multiple SLMs will be made available, for free!
- Azure AI Toolkit runs training data in Azure (where there is plenty of compute power) so that your local model can utilize the training result.
- Can replace GPT with a SLM, and fine-tune a dataset in a reduced period of time, all within VS Code and the Toolkit.

Following Paved Paths:

- Self-serve environments.
- Workflows and infrastructure should be available for development.
- "Start-right Templates" get you there.
- "Stay-right Governance" helps keep best-practices in focus.
- Shift-left notifications.
- Policy enforcement and security monitoring, as well as Observability within the App/service/solution.

Mark Weitzel Demo: Platform Engineering with Github Copilot & Azure

- Prefix Copilot Chat inputs with `@` to target Github Copilot Extension within Github Copilot.

## AI Everywhere Breakout Session

Accelerate software development from PC to Cloud.

Speakers:

- Brian Ehlert, F5 - NGINX
- Lior Kamrat, MSFT
- Ken Koyanagi, Intel
- Brian Rogers, Intel

Focusing on real world AI, and areas for growth:

- Efficiency
- Security
- Developer-ready
- Hybrid AI
- Ecosystem through partnerships

NGINX (Brian Ehlert)

- NGINX is now 20 years old.
- Began as a project aimed at solving the question of how to effectively handling 10,000 concurrent HTTP connections.
- Orgs struggle as they move to cloud, NGINX and Azure can help.
- NGINX-as-a-Service: Exclusively Intel and Azure! Paid offering, as opposed to NGINX open-source free tier.
- NGINX JavaScript helps with integration efforts.
- NGINXaaS: Just bring configuration, and it does the rest! Just select it in the Azure Marketplace.
- NGINX WebApp Firewall coming soon.
- NGINX Azure Kubernetes service offering(s) coming too.
- Intel OpenVINO uses NGINX to accellerate AI and provide failover and scaling availabilty features.

Microsoft (Lior Kamrat)

- Adaptive Cloud Approach means: How do we bring these technologies, developers, and clients together?

Intel (Ken Koyanagi)

- What is an AI PC? Uses NPU silicon in conjunction with CPU and GPU.
- NPU stands for "Neural Processing Unit".
- ONNX Runtime: Applications talk to the ONNX model, various extensions (exceution providers) include DirectML and OpenVINO, and output a result.
- EPs means "Extensible Execution Providers"

## Imagine Cup Finals

There were 3 finalists, 2 of them were particularly interesting to me:

- [RoadMap](https://www.planroadmap.com/)
- [FromYourEyes](https://fromyoureyes.app/) - who won the Imagine Cup, a cash prize, and a mentoring session with Satya Nadella!

The other finalist was a team that developed hardware to detect emissions in steel fabrication plants, integrated with AI. Great idea for sure, and I wish that team well.

Such a cool and inspiring event overall!

## Keynote - Tuesday

"Information at your Fingertips" - Bill Gates, 30 years ago. MSFT continues this vision, now with AI.

Now, the extension to that is "With AI, you can build what matters".

Highlights from Satya's keynote:

- The scale of the impact of AI is deeper and broader than previous significant technology changes (Azure, Win32, etc).
- 70 yo dreams: Can computers understand us? With more information digitised, can computers help us reason, plan, and act on all of this information?
- AI today represents significant break-throughs on both fronts.
- The rate of diffusion of technology (spreading around the world) is increasing.
- Pi-Silica: SLM provided in every Copilot PC.
- Windows Copilot Lirrary + on-device models using RAG, Vector
- Announcement: PyTorch Native and Web Neural Network powered by DirectML now supported by MSFT.
- MSFT "has always been a platform company...", enabling developers to build their own tools and applications.
- "On track to power datacenters 100% by renewable energy by 2024" :astonished:
- First vendor to support AMD ND MI300X-V5 silicon optimized for MS Azure workloads.
- Announcement: Azure Maia is new hardware now serving AI Prompts.
- Announcement: Azure Cobalt based VMs now available.
- 50k organizations now use Azure AI.
- GPT 4o allows inputs in multiple languages and also provides responses as such!
- Announcement: MSFT already provides many models, and at least a dozen more have been added including Hugging Face, in this case directly to Azure AI Studio.
- SLM: Small Language Model. Phi-3 is an example, and it has a half dozen or so models it leverages.
- Announcement: KhanAcademy will be using MSFT AI available.
- Announcement: AI-powered, Real-time Intelligence in Microsoft Fabric. Provides actionable insights.
- GitHub Copilot Workspace: Automates creating an Issue, then Specing, Planning, and Coding the solution.
- Announcement: GitHub Copilot Extensions - Customize capabilities from 3rd party services.
- Announcement: GitHub Copilot for Azure. Where are my resources? ... other questions can be answered.
- Demo: Using natrual language - Neha Batra VP Eng, GitHub did a demo using voice-command controlled Copilot development...in spanish!
- Announcement: [TeamCopilot](https://www.microsoft.com/en-us/microsoft-365/blog/2024/05/21/new-agent-capabilities-in-microsoft-copilot-unlock-business-value/) - Facilitiate meetings in Teams, take notes, collaborate with Chats, address unresolved Issues (work items), manage projects, etc, using your organization's information. Coming later in 2024.
- Looking forward: Copilots and Agents supporting many aspects of business processes and tasks.

Rajesh had some interesting canned demonstrations on Team Copilot, Copilot for MSFT 365, etc.

- Copilot Connectors allow users to go to a single source to get data from multiple sytsems.

Jeff Teper

- Copilot Extensions for _your Copilot_ for Teams, Sharepoint, and more.
- Creating a custom Copilot takes just a few clicks

Pavan Davuluri

- Qualcomm Snapdragon DevKit for Windows.
- Volumetric Apps: Partnership with Meta extends Copilot into Mixed-reality Apps - "VolumetricApps" and "VolumetricAPI".

Kevin Scott

- "Count on things getting more robust and cheaper over an agressive clip over time."
- Aim for things that are truely ambitious, as the next generation of tools become ubiquitous.
- Salman Khan was invited on stage to chat about AI, ChatGPT and Copilot.
- Turn concerns and risks into features that focus on the overall mission of the organization.
- Put up guardrails and constraints at the application layer to help drive safe, effective AI solutions and features.
- Khan Academy is going to provide AI Teaching Tools "to every teacher in the US".
- Khan says to focus on specific areas to make use of AI technology to move it and your project(s) forward, and to keep from becoming overwhelmed with (and overwhelming amount of) AI technologies.

## Resources

[.NET Announcements and Updates from Microsfot Build 2024 from the .NET Team](https://devblogs.microsoft.com/dotnet/dotnet-build-2024-announcements/).

[WinUI 3 Gallery](https://github.com/microsoft/WinUI-Gallery) simplifies style and performance enhancements for your WinUI 3 and WPF apps.

[Get Started with WinUI](https://learn.microsoft.com/en-us/windows/apps/get-started/start-here?tabs=vs-2022-17-10).

Windows Subsystem for Linux [(WSL) Documentation](https://learn.microsoft.com/en-us/windows/wsl/).

[DotNET 9 Previews (and eventually, releases)](https://dotnet.microsoft.com/en-us/download/dotnet/9.0).

[DotNET Aspire GA Announcement](https://devblogs.microsoft.com/dotnet/dotnet-aspire-general-availability/).

[Github Copilot for the CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli/about-github-copilot-in-the-cli).

[DotNET Apire Collections](https://learn.microosft.com/en-us/collections) on MSFT Leran.

[Windows Developer Center](https://developer.microsoft.com/en-us/windows/).

[AI Toolkit for Visual Studio Code](https://learn.microsoft.com/en-us/windows/ai/toolkit/) Overview (previously named "Windows AI Studio").

SLM: [Small Language Model](https://news.microsoft.com/source/features/ai/the-phi-3-small-language-models-with-big-potential/).

[Phi-3 SLM](https://azure.microsoft.com/en-us/blog/introducing-phi-3-redefining-whats-possible-with-slms/).

[Mistral SLM](https://mistral.ai/).

[ONNX Runtime](https://onnxruntime.ai/blogs/accelerating-phi-3) supports Phi-3 minim models across platforms and devices.

Direct Machine Learning [DirectML Overview](https://learn.microsoft.com/en-us/windows/ai/directml/dml): A low-level API that requires DirectX 12-compatible hardware.

[Microsoft 365 Blog article](https://www.microsoft.com/en-us/microsoft-365/blog/2024/05/21/new-agent-capabilities-in-microsoft-copilot-unlock-business-value/) about Microsoft Copilot's new capabilities.

[Intel Accelerator Engines and Intel AMX](https://www.intel.com/content/www/us/en/products/docs/accelerator-engines/what-is-intel-amx.html).

Take the [MSFT Learn Challenge](https://www.microsoft.com/en-us/cloudskillschallenge/build/registration/2024).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
