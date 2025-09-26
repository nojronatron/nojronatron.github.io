# Blazor Day 2025 Notes

Microsoft ASP.NET Team presented "Blazor Day" in 2024 to overview the Blazor framework. This event follows-up with the latest information on Blazor technologies, changes, and implementations.

## Table of Contents

- [General Notes About Blazor](#general-notes-about-blazor)
- [DotNET 10 (LTS) Focus Areas](#dotnet-10-lts-focus-areas)
- [Dan Roth - Blazor Improvements in .NET 10](#dan-roth---blazor-improvements-in-net-10)
- [Tim Purdum - Blazor Render Modes](#tim-purdum---blazor-render-modes)
- [James Montemagno - Production Deployment With GH Copilot](#james-montemagno---production-deployment-with-gh-copilot)
- [Blazor AuthN and AuthZ - Rocky Lhotka](#blazor-authn-and-authz---rocky-lhotka)
- [Exploring V5 Fluent UI Blazor Library - Vincent Baaij](#exploring-v5-fluent-ui-blazor-library---vincent-baaij)
- [Prerender and WebAssembly with Lazy Loading - Sergi Ortiz Gomez](#prerender-and-webassembly-with-lazy-loading---sergi-ortiz-gomez)
- [Designing for AI First - Ed Charbeneau](#designing-for-ai-first---ed-charbeneau)
- [From Onion to Clean Architecture - Johan Smarius](#from-onion-to-clean-architecture---johan-smarius)
- [Building Hybrid Apps with MAUI and Blazor - Beth Massi](#building-hybrid-apps-with-maui-and-blazor---beth-massi)
- [New in Blazor and .NET 10 - Jimmy Engstrom](#new-in-blazor-and-net-10---jimmy-engstrom)
- [VS 2026](#vs-2026)
- [Resources](#resources)

## General Notes About Blazor

- Originally shipped in .NET 3.0 Core!
- Enable devs to build rich, performant web apps using .NET
- Fast release cycle over the last 5 years
- Blazor was based on Razor, the HTML templating language for browsers
- Naming? B(rowser)l(r)azor
- Can integrate with other frameworks: Angular, React, etc
- Blazor is "a fancy JS app if you just squint at it" (Dan Roth)
- Blazor works with the Open Web Ecosystem

## DotNET 10 (LTS) Focus Areas

For ASP.NET Core:

- Security
- Observability and Diagnostics
- _Targeted_ performance improvements
- Address "top pain points & gaps"

_Note_: 3 years of support for LTS.

## Dan Roth - Blazor Improvements in .NET 10

Blazor:

- NotFound.razor now included in the WebApp template
- Uses standard ASP.NET Core Middleware helping trigger 'not fount' middleware and handling (with correct 404 code response)
- Layout includes `ReconnectModel.razor` that enables customizing the 'reconnect' UI when web socket connection is latent/broken
- Rendermode `@rendermode InteractiveServer` declaration applies at the page level
- Identity: Includes support for Passkeys! ("move away from passwords 2.0")
- DB Migration still not automated, however:
  - Web UI still has a 'migrate now' link in debug mode
  - It is possible to set automated migrations for production in GH Actions, Azure Pipelines, Dockerfile, etc
  - Also, manual migrations can be executed for local, cloud, and other hosted scenarios using PoSH or other scripts

Blazor Monitoring and Orchestration:

- Use Aspire! R-click Project in VS and select menu 'add Aspire Orchestration Support'
- Open Telemetry: New Meters and Trace Sources will be added to Blazor Template with the release of .NET 10
  - Until then, there is open-source code available to do the same
- Aspire Dashboard is _built using Blazor_
- Azure App Insights-like metrics available via Aspire (more added with .NET 10)
- Traces have been improved: Reworked Name and Timestamp views, including drill-down click-in details

Blazor State Persistence in Blazor Components:

- Declare the state(s) you need persisted
- Background:
  - Prerendering generates static HTML first _then_ rerenders with state information
  - This causes the client to call for the state data _twice_
  - Persistence allows Blazor to store the pre-rendered data state
  - The re-render cycle picks-up the persisted state data and uses it instead of querying for new
  - Use `[PersistentState]` attribute on the Property that needs to be persisted
- Disconnected Circuit State persistence:
  - Enables minimizing browsers (or moving away from a mobile app) without losing its state
  - Frees-up Circuit and server-side resources without losing the State
  - To implement: Add JS using new Blazor API to handle 'document.hidden' state when 'visibilitychange' event is fired

## Tim Purdum - Blazor Render Modes

Presenter: Tim Purdum, Dir Prod Dev, Dymaptic

### Modes

Static:

- As of .NET 8. Pages render Components and are sent to browser as static HTML with JS and CSS
- Get, Serve, done!
- Navigation supported
- Useful for low-resource needs, full-page load scenarios
- ASP Classic, WebForms, MVC, Razor Pages, static HTML
- No Lifecycle Methods are called
- Event Handlers using `@` _do not fire_

Interactive:

- Lifecycle Methods included
- Signal-R 2-way channel (web socket) between client and server
- Continuous interaction channel
- Live data-binding
- Realtime page updates
- JS Interop enablement
- Datastore access _is_ available (however not recommended for production)
- Network lag introduced

Interactive Web Assembly:

- No web-socket
- Specific DotNET RunTime downloaded to the Client Browser
- Browser handles all rendering and interaction _within the browser iteself_
- Client web API calls, SignalR, and gRPC _must be set up separately_
- Live data-binding
- Real-time Updates
- JS Interop
- WASM is _single threaded_ (just like JS)
- Asynchronous programming supported, however UI deadlock is more likely than with Server Interactive mode
- Slower first-page load
- Subsequent loads are _very fast_ (no network latency)
- Similar to React, Angular, other SPA frameworks
- Standalone WebAssembly project and Blazor Web App project are supported as "Interactive Web Assembly"

Interactive Auto:

- Runs from server on first load via SignalR
- Web Assembly downloaded in background
- Next load switches to Web Assembly Interactive version
- Better response on initial connect
- Conections and communication pieces _must be developed separately_ to support _both_ WebAssy and SignalR-based rendering modes

Blazor Hybrid:

- Not technically a Render Mode
- Runs in WebView in .NET MAUI
- Is _not Web Assempbly_
- Multi-threaded code
- Access to device APIs (via MAUI framework)
- Component reuse in Web, Desktop, and Mobile platforms (via MAUI)
- Set up a Shared Library to define the application then use Platform code to implement WinUI, Web UI, and Native/Mobile
- Always set Hybrid to interactive (this fires OnAfterRender() methods)
- _Note_: Does _not_ require setting `@rendermode`.

ASP.NET Core Razor vs. Blazor:

- Razor Syntax: `.cshtml`
- Blazor Component: `.razor`

Page vs Component:

- `@page` routing declaration: Page
- No `@page` declaration: Component

More About WebAssembly Project:

- Interactive Auto or Interactive Server still work
- WebAssy Client can "see" the entire WebAssembly Project (it is loaded into WASM on the client browser)
- Non WebAssy Project must be contacted by other means e.g. HTTP API calls, etc
- Use a Razor Class Library:
  - All references flow "up" to the Server
  - Client can also see the references

Add Interactive Render Modes:

- Must edit `program.cs` (?)
- Include Service References
- Use `@rendermode` at top of file
- When declaring a component `<ComponentName @rendermode="InteractiveServer" />`
- Can be declared at the `<Route>` element level to set Render Mode to entire site
- Render Mode inheritance dribbles down to child Components
- `@RenderInfo.Name` is new as of .NET 9

Razor Component Lifecycles:

- In any case, a Component Render Lifecycle only triggers _after its parent_ completed a Render Lifecycle
- Static Page: OnFirstRender, OnParametersSet, DOM Updates
- Interactive Modes: OnInitizliaedAsync, OnParametersSet, Render, DOM Updates, OnAfterRender

Patterns and Techniques:

- Prerendering: Rendered on server first
- Prerendering pattern to avoid: Iterating and other possible looping code
- Stream Rendering: Use `@attribute [StreamRendering]` directive, handle async operations with `async` and `await`, prioritize Layout rendering before data is streamed in

Identity Framework and Rendering Modes:

- Use the latest version of the Identity and InteractiveAuto Mode to get all the code

## James Montemagno - Production Deployment With GH Copilot

Principal PM Lead Developer Community, MSFT

"Vibes all the time!" - James Montemagno

James has built and shipped 4 Web Apps using AI!

GH Copilot can help with all aspects of "being a developer":

- Less than 20% of time is statistically "coding time"
- Make robots to the dirty, dull work.
- Copilot can be told to write _all the code_ from start to finish!
- "Give in to Agent Mode" to make all the coding happen.

Takeaways:

- Improve prompts
- Add context
- Draft up ideas
- Create a plan
- Have Agent Mode execute the plan
- Iterate over the plan

Focus on Context using Copilot Instructions:

- Project structure
- Styling
- Theming
- Blazor and .NET specific instructions
- Tell the Agent which files or file-types to apply specific instruction to

Chat Modes:

- Set into "design" mode or "planning" mode to set a "system prompt" that helps guide prompts

Prompting:

- Reusable system prompts
- Output requirements
- Define parameters and dependencies and injections and lifecycles

MCPs:

- Additional context applied via MCP Server calls
- Create GitHub Tasks to guide the project process

Models:

- Various experience and capabilities with each model
- Terse vs exploratory vs verbose vs creative vs pedantic vs local
- Use branching to freely commit solutions various Models provide (you can always use PRs to decide which Model's solution to use)

Async Agents:

- Background Agents handle tasks while you doing other things
- Github Copilot on the Github website is a prime example
- Implement bugfixes, feature requests, etc

## Blazor AuthN and AuthZ - Rocky Lhotka

Rocky:

- VP Strategy, Xebia
- Chief Architect at Marimer LLC
- MS MVP

Models:

- Oauth: EntraID, auth0, okta, etc
- DB/LDAP server: Internal credential verification
- Individual accounts: Users, roles in a DB (1990 vintage, and utilized in ASP.NET classic through today including Blazor)

User Principal:

- AKA "Identity"
- Claim Objects: User profile, roles, tokens, etc
- ClaimsIdentity: Wraps around Claim Objects (user name and other metadata)
- ClaimsPrinciple: Wraps around ClaimsIdentity. This is what Blazor manages

Blazor Authentication:

- AuthenticationStateProvider => AuthenticationState => ClaimsPrincipal
- Built and implemented using DI container services
- Many layers of abstraction to simplify the AuthN and AuthZ flow in Blazor, and ensures common pieces are always there without having to implement or directly wire it up
- Simply use the OOP abstractions to leverage the provider needed!

ASP.NET Core Authentication:

- HttpContext: Sign-in, Sign-out APIs (note: via HttpContextAccessor)
- Identity persistence: Cookie, URL, plus others
- Identity hydration: Recreate ClaimsPrincipal upon every login event, store in AuthenticationState

WebAssembly and MAUI:

- Different world than server side!
- All clients vulnerable to hacking (if you have physical access to the resource, you own it)
- Process: Call service to validate creds, create ClaimsPrincipal/ClaimsIdentity (based on service call), then store ClaimsPrincipal in AuthenticationState (implemented via custom AuthenticationStateProvider)
- Developer _must_ set ClaimsPrincipal and send it back to Blazor, on demand

Notes:

- Can bring in HttpContext using `builder.Services.AddHttpContextAccessor();` in DI
- Add Authentication (and configure it) also in DI
  - Schemes, cookies, and much more can be configured
- `AddCascadingAuthenticationState()` - a Blazor Auth feature
- User Validation Service can be used to validate credentials:
  - This is written by the App Dev for client-side validation
- `App.Use Autehtntication()` and `App.UseAuthorization()` must be enabled in Blazor DI
- `App.Razor` gives way to `Routes.razor`, where `<CascadingAuthenticationState>` can wrap `<Router>` to ensure access is available on childe pages. `<AuthorizeRouteView>` enables setting user Roles and Claims to child Page/Components
- Enable ability to view username etc: `@using Microsoft.AspNetCore.Components.Authorization` at top of page and then add `<AuthorizeView>` element to the page along with `<Authorized>` and `<NotAuthorized>` to display proper page information (or Page/Components) to the user based on their Authentication state
- Non-interactive login-page requires "postback" from the server to enable authentication.
- _Avoid using HttpContext_ in interactive render mode pages!
- `<EditForm>` works in Static _and_ Interactive Render modes. Ensure `FormName` attribute is set
- `[SupplyParameterFromForm]` enables using "PostBack" to drop the `UserInfo` instance into the page UserInfo Property
  - From this point on, APIs enable access to validate the username and password, create claims identity, add claims and add user to roles, etc
  - Lastly, sign-in the user occurs

## Exploring V5 Fluent UI Blazor Library - Vincent Baaij

Vincent Baaij: Principal Fluent UI Blazor Maintainer at Rubicon Cloud Advisor, previous MSFT employee

What is Fluent UI for Blazor?

- Web Components: Create custom html elements with independenty styling, private DOM, attribute change detection, and theme/skin support
- FAST: Techns enable building web-standards-complient Web Components, ready for front-end frameworks (ncluding Blazor)
- Fluent Design System (Fluent): Aligned with MSFT Design Guidelines (Aero, Metro, Modern/Win11). Light, depth, motion, material, and scale. Implemented as a set of UI components: Reusable, customizable, responsive, modern. Tied closely to design standards, not flashy, creative UI design
- Completely Open Source
- Follows ASP.NET Core namespace (but is not MSFT nor DotNET Foundation driven)
- Support only available via the Fluent UI for Blazor GitHub Repo
- Layouts, Grid, Stack, various Input elements, and many other event-y and responsive Components
_Note_: This could be good to experiment with for Blazor Hybrid projects

## Prerender and WebAssembly with Lazy Loading - Sergi Ortiz Gomez

WebAssembly Headaches:

- First Load Time: Slow. First render is server-side while WebAssy downloads
- SEO Featuring: Website is just one HTML file in WebAssembly, so not rendered for crawlers

Prerender and Lazy Loading:

- Improve startup speed
- Reduce initial download size
- SEO available with first request

How to Fix:

1. Server-side app
2. Blazor Client
3. Define what libraries not needed on 1st load
4. Define SEO logic to add to app

Server-side App:

- Backend should create WEb API for pre-rendering Blazor App
- Often done using Minimal API
- RazorPages and MapRazorPages, WebAssempbly.Server, UseStaticFiles, and then add `_Host.cshtml` (usually within the `Pages` folder)
- Map FallbackToPage `_host` to root page
- Add references to Blazor WebAssembly app
- `_Host.cshtml` must reference CSS file(s)
- Blazor JS Load must call `BlazorWebAssembly.js`

Blazor Client:

- All needed services in Blazor App should also be available to Client, using DI Container (e.g. `GetRequiredService<IInterface>()`... etc)
- Remove "root component" labeled `#app` and "head outlet" `head::after`
- Delete `index.html` from wwwroot directory

Lazy Loading:

- Load extra DLL from extenral deps only _after_ initial page render
- Reference into the `ItemGroup` element from teh project file e.g. `<BlazorWebAssemblyLazyLoad Include="{Assembly_name}.wasm"/>`
- Reflection, `AdditionalAssemtlies`, and `LayzLoadedAssemblies=new()` are required in order to implement them in `@code{}` within the `App.razor` componnet

SEO Logic:

- Create logic for viewing within a rendered page i.e. the Razor page within the Host
- Optionally create SEO logic within the WASM project
- Web API render from server-side page
- Page title should be nae of requested page
- After first render, _then_ load WASM page

## Designing for AI First - Ed Charbeneau

Ed: Dev Advocate, Progress Software

Natural Language UX with Blazor

Problems with Current AI Integration:

- Demos are very basic, chat completions
- LLM's are brains behind NLP, and basic chat page doesn't demonstrate that

Smart UI Components:

- Take existing Components and add AI improved features
- Customize auto-complete based on app capabilities and actions being performed by the user

Smart AI Search:

- AI embeds vectors with embedded meanings
- Queries are by relationship, not just verbatim text

LLM Beyond Chat:

- Translate text
- Code generation
- Launguage-to-language tranlation
- Work with relational data

LLM Inputs and Outputs:

- Ins: Code, schemas, text, unstructured data
- Outs: Code, translated text, structured data
- Combine INs and OUTs for best experience, capability, results

So why not just ask your Filtering Form what it can do and how to use it?

- AI must be told how the form works
- AI must understand the data in a way where interactivity is possible

Ed presented "State-based Control Strategy":

- Describes the state of the UI component
- Describes the state data
- Describes the query the user has input

Ed demoed a Blazor-based WebApp, augmented with State-based Control code:

- Interactive using keyboard or voice
- User doesn't need to know site navigation, form layout or usage
- User not required to fumble through filters, sorting, or pagination on data tables andn forms of all sorts

## From Onion to Clean Architecture - Johan Smarius

Johan - Lead MSFT Dev consultant (and much more).

Onion Architecture:

- Separation of concerns
- Extensibility
- Testability
- UI Independency
- Independent external components (e.g. Database service)
- Dependencies run from outside to the inside
- Object models witin teh APp core
- Object services next inner layer
- Application services next outer layer
- UI, Tests, and Infrastructure (interfaces) in the outermost layer
- Services can become pretty large

Clean Architecture:

- Entities in the core
- Use cases wrap the core
- Controllers, Gateways, and Presenters wrap use cases
- Devices, Web, UI, and DB and other external interfaces are on the outside layer
- Flow of control looks more like DI
- More abstract: Closer to the core
- More likely to change: Further outside layer
- Do not pass Entities to the callers, use DTOs instead!

Conclusion:

- Start _simple_, worry about complexity and architecture design a little later
- Migrate to a design architecture as early as practical (Onion or Clean)
- GH Copilot can help with migration (use branches to manage change, implementation)
- Avoid over-engineering
- Choose an architecture that fits the need
- Either Onion or Clean architecture will assist with moving between Server and WASM types

## Building Hybrid Apps with MAUI and Blazor - Beth Massi

Beth: Principal Product Manager on .NET MAUI Team, MSFT

Choises for client app dev:

- More reach or deep native experiences?
- Blazor: Websites and PWAs for most reach
- MAUI: Cross-platform _native_ apps
- Hybrid: Blazor and MAUI for wide reach _with_ native feature capabilities

DotNET 10 Investments for .NET MAUI:

- Quality
- Performance
- Simple
- Modernality
- GA Nov 11th during .NET Conf!
- Aspire Support for MAUI
- More granular control in hybrid Blazor Components
- Hot Reload improvements
- Hooks for added control over Hybrid and Blazor WebView components
- MAUI will have its next release _just prior to .NET 10_ (late October?)

_Note_: Syncfusion releases OSS controls for .NET MAUI, and is part of the .NET MAUI Github team.

- [Syncfusion MAUI Toolkit](https://github.com/syncfusion/maui-toolkit)

What are Hybrid Apps?

- Blend native and web technolgies
- Application core is written in HTML
- Wrapped Native Container provides APIs for native access
- Code reusability across web and mobile
- Mobile ecosystem/Store distribution (MSFT, Google Play, Apple app stores)

Blazor Hybrid:

- MAUI provides Native Container
- WebView used for _fully native web UI_, derived from plaform "WebView"
- UI does _not_ require internet (all client OOB is packaged with the app)
- Blazor input controls, validation, forms and auth are all built-in
- MAUI abstractions enable multi-platform (Windows, Android, Mac)
- Supports other JS Frameworks (Angular, React, Vue, etc) _with_ all the benefits
- C# and JS interop included

Structure:

- Project: `dotnet new maui-blazor-web`
- Add shared Razor Class Libraries across Web, WinUI, and Native(mobile) Projects

General Notes:

- Use .NET MAUI Blazor Hybrid and Web App: Provides a SOLUTION template with 3 projects (4 projects when WASM is selected)
- `dotnet new maui-blazor-web`
- App References are pre-wired
- Includes various shared resources including MAUI platform resource wirings
- Device-specific code can be written in teh `Platforms` directory
- Root Project dir contains a single MAUI (WPF-like) App ContentPage type with a RootComponent at the `<Selector="#app" .../>` element
- Shared RazorClass Library should be used to enable all capabilities for WinUI, Web, and Mobile
- MAUI Hybrid Apps _are always interactive_ at the Project level
- RazorClass Library only needs access to interfaces (abstractions) and doesn't need to know implementation details for the platform and UI (separation of concerns, write-once and target multiple platforms)
- Use a ReverseProxy (built-in to VSCode, Visual Studio) to allow Virtual Phone to work with running App in Debug mode
- Use _Compiler Directives_ to display the correct UI
  - Be sure the CSPROJ file targets the correct Frameworks to get these directives to be effective

Fluent Blazor Hybrid exists

## New in Blazor and .NET 10 - Jimmy Engstrom

Lead Developer, MVP, CodingAfterWork.com, Dometrain, and several Blazor books

Visual Studio 2026 Features:

- Roslyn Cohost Server: Razor and Roslyn don't always agree on the state of your code. Razor now runs on Roslyn, to avoid these inconsistency issues.
- New Project Templates: Aspire, DotNET MAUI, ...
- Blazor Web App: Updated to support Aspire enlistment, various Rendering (server, individual, auto interactivity) Modes, etc.

Blazor Components:

- `<AppPreloader />`
- `<ImportMap />`
- `<ReconnectModel />`: Direct access to the message Blazor Framework displays when it loses WebSocket/SignalR connectivity
- `@Assets[]`: Fingerprinted for proper caching
- `Routes.razor`: NotFoundPage="" points to a speicifc `@page "/not-found"` to provide custom page for this scenario
- WASM fingerprinting is available in .NET 10

Secure Blazor Apps:

- Support passwordless AuthN with Pass Keys and OAuth
- Hybrid Auth integration into existing apps (upgraded to .NET 10 SDK)
- PassKeys are compatible with Individual Accounts

Aspire:

- Add OTEL Telemetry metric resources via DI

WASM Project Features:

- Profilers can be enabled within the web browser within the WASM Project CSPROJ Includes declarations
- Enables DevTools to profile WASM events, metrics, network and processing, etc
- Diagnostics: JS tool collects metrics to a file and VS 2026 can process and analyze

Blazor State Persistence:

- Content pre-renders when using the WebApp template. SignalR didn't have an automatic transfer from pre-rendered to WASM. After first-load, future page renders speed up Prerendered Web Apps and WASM usage
- Switch from Static to WebAssembly causes data state to change (in some cases) _and_ it causes the screen to visually re-render or flash causing poor UX
- PersistentComponentState requires a bit of code to set it up and use it
- DotNET 10 introduces attribute `[PersistentState]` that enables checking for null on the data fetcher to determine if a state already exists
- Once the prerender completes and WASM takes over, the data _is already in place without having to refresh it_
- Works for dis-reconnect SignalR events, maintaing state through connection problems

Blazor Circuit Persistence:

- Enables storing state when a SignalR circuit "is not needed" to save on server-side resoruces
- Enables resuming state from a sleeping UI/Application (with a closed SignalR circuit)

## VS 2026

- UI Improvements
- Performance improvements
- Currently Insiders Channel only, however release is slated for (.NET 10 release?)
- Project templating is the same (no surprise)
- Theming makes it look neat

## Resources

- [Get .NET 10](get.dot.net/10)
- [DotNET Core What's New on MSFT Learn](learn.microsoft.com/dotnet/core/whats-new)
- [.NET Roadmap](aka.ms/dotnet/roadmap)
- [.NET AI](dot.net/ai)
- [.NET Apire](dot.net/aspire)
- Links to Rendering Modes in Blazor from [Tim Purdum's Website](https://timpurdum.dev)
- [Fluent UI for Blazor](https://fluentui-blazor.net)
- [Getting Started with Fluent UI Blazor Library](https://youtu.be/lUZ5mrg2Q8k) video
- [Telerik](https://telerik.com)
- [DomeTrain](https://dometrain.com)
- [CodeMag](https://codemag.com) by the Code Group
