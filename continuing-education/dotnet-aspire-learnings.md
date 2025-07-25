# DotNET Aspire Learnings

Notes from my learnings about this MSFT Framework for .NET 8 and newer.

Releases (for reference):

- v9.3: May 2025
- v9.2: April 2024

**Note**: Not all content captured below spans all releases listed above.

## Table of Contents

- [DotNET Aspire Developers Day](#dotnet-aspire-developers-day)
- [Hands-on with MS Learn](#hands-on-with-ms-learn)
- [DotNET Aspire Tooling](#dotnet-aspire-tooling)
- [Aspire Limitations and Gotchas](#aspire-limitations-and-gotchas)
- [Microservices and Aspire](#microservices-and-aspire)
- [Service Discovery](#service-discovery)
- [Caveats Of Note](#caveats-of-note)
- [Resources](#resources)
- [Footer](#footer)

## DotNET Aspire Developers Day

This full-day event will overview .NET Aspire and dive in to use cases and implementation details from 0900 to 1600 PDT on 23-July-2024.

### Keynote

Presenters:

- Maddy Montaquila
- Glenn Condron

> Your building blocks for cloud development.

App needs, Aspire Delivers:

- Observability: Metrics, DI integration, Logging support, Enrichment, Redaction, Fakes testing and metrics.
- Resiliency: Polly-based resiliency packages, SignalR Stateful Reconnect.
- Scalability: AOT, Performance, Chiseled Ubuntu.
- Manageability: Certificate auto-rotation support in Kestrel.

Basic Cloud Services today at minimal require:

- Blazor App as the WebApp
- Backend API(s): Identity
- Database(s)
- Potentially AI

Anything more than basic cloud services contain many frameworks and services and are usually very complex.

Aspire Stack Features:

- Smart defaults
- Orchestration
- Components
- Developer Dashboard
- Service Discovery: For example, Aspire will automatically resolve API Endpoint URLs by name in the DI Container.
- Deployment

Aspire Use Pitch:

- Easy to start: OSS, Templates, Components
- Easy to build: Service discovery, developer dashboard, logs, metrics, distributed traces, all just by adding an Aspire project.
- Easy to deploy: Single command run, App topology in C#, Cloud deployment support.

Aspire supports other language projects too!

Add Aspire To An App:

1. Have an existing app.
2. Add an Aspire AppHost project.
3. The Aspire Project creates an interface that provides logging, tracing, and various other features to help manage the existing app project(s).

Obviously, there's a bit more to it, but the above is the general idea.

_Announcement_: .NET Aspire 8.1 officially released 23-July-2024

### Enhance Business Processes with .NET Aspire and Generative AI

Presenter:

- Steve Sanderson

What about experiences other than Chat Bots?

- Semantic Search: Instead of using a simple search textbox, enable AI-backed search results by adding Semantic Kernel and backing models with added Context to allow searching manuals or other data sources.
- Summarization: Adding .NET Aspire enables rapid access to Logging and Insights including WRRC/REST circuit and other behavior.
- Typeahead
- Auto-categorization
- Classification
- Evaluation: What is the quality of the system? How is this performing over time? Can these factors be quantified? Usually this is done with test data sets.

> What are my users _really_ going to use?
> How can I develop measureable features in this solution?

### JavaScript/Node with .NET Aspire

Presenter:

- Chris Noring

Problems Aspire Attempts To Fix:

- Not easy to build distributed apps: Many components and configurations, caching and DB connection issues, etc.
- Resiliency and telemetry are complex but necessary for a production system.
- Reinventing the wheel, or just writing the same code and using the same system over and over again?
- Docker containers with many moving parts, or multiple containers used to assemble a system.

Key Aspire Features and Components:

- Service Discovery
- Telemetry
- Resilience
- Health Checks

Aspire Use Cases:

- Observable, production-ready distributed applications.
- Cloud-native Apps that Scale.
- Enhance local development experience, provide abstractions to streamline setup and service discovery, and ensure consistent setup patterns across apps.

More About Orchestration:

- App composition: Specify projects, containers, executables, and cloud resources that make up the application.
- Service discovery and connection string management simplify service setup, configuration, and management.

Core Concepts:

- App Host: Central Project. All orchestration and service registration happens here.
- Starter App: Your project!
- Service Defaults: .NET Aspire project configurations.

Prerequisites:

- DotNet 8.0+
- DotNet Aspire Workload (`dotnet workload install <workload_id> ...`)
- OCI compliant container runtime (Docker Desktop or Podman)
- IDE like VS or VS Cdoe with C# Dev Kit Extension

Scaffold The Project:

- Command Palette
- Terminal: `dotnet new aspire-starter`. Run the Application from `AppHost` project to get all Aspire features running alongside the sample App.
- Visual Studio right-click menu

Starter Template:

- Contains all necessary Aspire projects and components
- Also has an example app that can be extended.

Important AppHost Project Components using the Aspire Manifest:

- Program.cs
- aspire-manifest.json
- Manifest can be updated: `dotnet run --publisher manifest --output-path path_name`
- Consider the Manifest to (loosely) act like a Node Package.json file.

Projects are added to Aspire in the DI using `AddProject<T>` and defining a default string name.

- Use `.WithReference`, `.WithHttpEndpoint`, `.WithExternalHttpEndpoints` methods to configure the Aspire-registered Apps

### .NET Aspire with MongoDB

Presenter:

- Luce Carter, Dev Advocate, MongoDB

MongoDB, ConsmosDB

- MongoDB is a key-value documents database (rather than tables) and supports other data types. General purpose. No-Sql. Flexible schema. Supports _horizontal scaling_. On-prem and cloud-service based.
- Atlas used to be cloud-only, but has been extended to an entire suite of services for both on-prem and in the cloud. Includes device SDKs, Charts for simplex visualizations, Analytics including Power-BI connectors, and Text and Vector Search features.
- Availability through failover, Flexibility through schema changes and validation, Scalability both vertically and horizontally (benefit over SQL DBs - MongoDB uses `Sharding` to scale this way), and readable data (binary JSON but displayed as JSON text documents).
- MongoDB Atlas in MS Azure includes a Pay-As-You-Go tier (as close to free is you can get).
- CosmosDB is an emulated flavor of MongoDB.

MongoDB with .NET Aspire

- `IMongoClient` in DI Container registration makes this available.
- Can be used as a Container as part of the solution, or can point to an Atlas service.

### Database and .NET Aspire "DAB"

Speaker:

- Jerry Nixon

Demo:

- Empty Aspire Project using all defaults.
- Only AppHost and ServiceDefaults project exist.
- Use SQL Server Object Explorer and create a new DB with new table(s).
- Create a DB Project using SQL Server Object Explorer and point it to the Aspire-enclosing Solution.
- Back in VS 2022 the DB Project will be included. Use `Publish` menu to push schema changes back to the SQL Server.
- In VS 2022 Pre- and Post-deployment scripts can be included to do things like Seed the DB with data.
- Create a folder in the Database Project called Data, then use the Database to generate SQL Scripts. Ensure to turn-off the Build Action for these files. _Remember_: Review the generated script(s) to ensure they do what you intend them to!
- Add the Sql Scripts folder to the `.gitignore`.
- Select Add .NET Aspire Package while AppHost is selected, and chose AspireHosting.SqlServer.
- Build-out AppHost to add SQL Server, set a known password with `builder.AddParameter("sql-password");` and pass that in to the `builder.AddSqlServer()` method.
- Use AppHost to open "Manage User Secrets" and include a Sql Password for authentication. Remember to add the connection details to `127.0.0.1,port`, using SQL Auth, and use the password that is set. Redirect `builder` in AppHost to build the Connection String.
- Build the shell files necessary for a Linux container into the Aspire AppHost project and store it in a folder named something like `sql-server`. Update the scripts to be used for a Linux container, verify the script contents to ensure they do the correct things. These scripts will get called by Aspire to build the DB into a Container.
- Persisting data across debug sessions requires creating a volume using `.WithDataVolume()` method. See Docker Desktop to see the volumes change when the Solution is run. Docker volume mounting enables loading the persisted SQL data!
- Enable container building within `builder` in the AppHost Program.cs.
- DataApiBuilder: New tool used to build MS Sql container in Development Mode using Terminal commands. Remember to use the command to reference the tables to be used by the Application.
- Now the Connection String must be referenced in AppHost builder: `.WithReference(sqlDatabase)`.
- NuGet "WaitForDependencies" package will become available soon, which ensure Aspire-containing Solutions will wait for dependencies like SQL Server to be "ready" before attempting to connect.
- Create a new Project to consume the Data API.
- Add the project to orchestration by using Menu Item to "Add to Orchestration" and references will get set.
- Back in the AppHost builder, include `.WithEnvironment()` to set the data api url parameters.
- Add another `.WaitFor()` so that the new project consuming the data api waits for dependecies to start before it is accessible.
- When publishing via Aspire, it should be set to _prompt for connection information_, rather than using the dev/debug connection settings.

### Taking Advantage of .NET Aspire to Build Event-Driven Apps Using CQRS

Speaker:

- Santiago Arango Toro

I took a break during this presentation. Notes will be added later if/when the presentation is available for future review.

### Components

Speaker:

- Eric Erhardt

I took a break during this presentation. Notes will be added later if/when the presentation is available for future review.

### Secrets, Security, and Key Cloak

Speaker:

- Jeremy Likness

Authentication:

- MSFT Entra
- Auth0
- KeyCloak!
- ...more.

Authorization:

- Add and Use Authorization within the configuration builder (i.e. ASP.NET Core Authorization).
- For each Mapped Endpoint, add extension method `.RequireAuthorization()`.
- Get the Access Token (and refresh Token) from the Authentication Provider and test using CuRL or similar.

Secrets:

- Passwords, Connection strings, etc.
- Use a Managed Identity like Azure ID (Entra?)
- Use X.509 Certificates!
- Long strings of characters like HEX encoded or better, but not as secure as Managed IDs or Certificates.

KeyCloak:

- Keep app secrets secret!
- NuGet package, just reference it in your project file as an Includes.
- Realm: A group of related applications.
- Includes extension methods to allow passing a KeyCloak configuration to `builder.Services`, e.g. `AddKeycloakWebApiAuthentication(callback)`

Hierarchy of Secret:

- Don't use them if you don't have to!
- Secure Vault: Azure KeyVault, KeyCloak vault, others.
- Store encrypted.
- _Never_ hard-code or store in plain-text with the project.

Secret Parameters:

- Used to supply secrets to modules that know how to access the params.
- Aspire will encrypt these for you.

### Deployment Options for .NET Aspire Apps

Speakers:

- Brady Gaster
- Maddy Montaquila

Flexible Integrations and Deployment:

1. Create and update your Aspire-based app.
2. Right-click Publish, which leverages AZD under the hood.

Compare this to doing your build and deploy operations project-by-project, especially for larger, production deployments.

CI-CD Aspire with AZD Demo:

- Start with an existing project.
- AZD Init: Use a template or existing code (the latter in this case).
- Allow creation of an environment that includes .NET Aspire.
- Also demoed using GitHub Actions to leverage AZD to deploy to Azure from the GitHub repo, rather than from the dev workspace.
- .NET Aspire Workload must be included prior to any CI-CD deployment job (just like any other Workload).

Aspir8

- Brady demoed using this cmd-line utility to setup and deploy Aspire projects to Docker instances and cloud-hosted services.
- Not only can Aspir8 create, it can also _destroy_.
- Aspir8 supports Kubernetes!

### .NET Aspire Dashboard and Telemetry

Speaker:

- Leslie Richardson, Sr. Product Manager, DotNET, MSFT

> Focus on Telemetry, using the Dashboard to gain insights into your App.

_Note_: There is a _standalone dashboard experience_ available from .NET Aspire!

Dashboard Exploration:

- One-stop-shop for monitoring, endpoint inspection, and insights, powered by OpenTelemetry.
- Resources: Containers, projects, executables, and DB data. Resource states, event timestsamps, and environment variable listings, as well as errors. Also has links directly to the endpoints served by the solution!
- Console Logs: Select which resource to view results.
- Structured Logs: Drill-in to specific logs, view by resources, filter by error or other log entry type, etc.
- Traces: Lists all activities spanning all Application processes including REST, DB activities, etc. Provides timeline views, timings for actions, WRRC turnaround, and associates these actions with the compoennts that are talking and listening. There are also basic resource statistics views for each App.
- Open Telemetry: OTEL SDK is the layer that all information passes through, and the means by which Aspire generates Dashboard interface.
- Support for Application Insights as well as other APMs like Splunk, Graphana, etc.
- The Dashboard is stateless and targets design and debug-time, and is not designed for in production implementation, _however_ all of the monitoring via OpenTelementry SDK is _still emitted_ so that the hosting service can capture that telemetry.

Create Your Own Metrics!

- Add custom meter for metrics: Define a counter and name the metric with a description, add an `ActivitySource`. Add custom logging by including the `ILogger<Program>` parameter into the `app.MapGet()` endpoint, then call `StartActivity()` referencing the `ActivitySource`, then add a `SetTag()` call that date-time stamps and sets a summary, then call the `LogInformation()` method. Lastly, add `.AddMeter()` to `.WithMetrics()` extension, calling the custom meter, and also `.AddSource()` to the `.WithTracing()` extension.

### Production Grade Observability with Azure Monitor Application Insights

Speaker:

- Matthew McCleary

I took a break during this presentation. Notes will be added later if/when the presentation is available for future review.

### OpenTelemetry with New Relic

Speaker:

- Harry Kimpel

Modern observability business objectives:

- Maximim uptime
- Optimize business
- Innovate faster
- Operational efficiency

New Relic:

- All-in-one observability platform.
- Metrics, Events, Logs, Traces, and 3rd Party Telemetry.
- Pure SaaS cloud service.
- Special note: High Cardinality - associates issues with users, products, or other custom attributes to help with root cause analysis.

### .NET Aspire Internals and Extensibility

Presenter:

- Mitch Denny, .NET Aspire Team Dev, MSFT

Note: Aspire Test Projects can be added individually to an existing Solution.

The Layers of .NET Aspire:

- Generally launched via an IDE.
- AppHost executable leverages Application Model to describe the Application.
- Application Model starts-up the Developer Control Plan which launches the Aspire Dashboard.
- Aspire Dashboard returns information to AppHost.exe.
- Reverse Proxies and other local processes are launched from the Developer Control Plane.
- Container Runtime and its containers are launched from the Developer Control Plane.
- Telemetry from Local processes and Containers are sent to the Dashboard.

Extensions:

- Add and With-prefixed methods added to builder within the DI container are the Aspire Connections implementations.

.NET Aspire Primitives (key concepts):

- Small number of building blocks.
- Orchestration of these building blocks controls how an Application launches.
- Resources are set via Annotations in the core, so building Extensions are built upon those annotated Interfaces.
- Many `IResourcesWithx` interfaces within .NET Aspire define its ability to interoperate with the App Builder container.

Distributed Application Lifecycle Rules?

- Interface IResource: A core contract in app lifecycle.
- IDistributedApplicationLifecycleHook interface: Has some default implementations. Provides a contract for adding service references to .NET Aspire for registration with reverse proxies and thus, reporting/telemetry?
- .NET Aspire is built on top of IContainer, enabling plenty fo opportunity to extend it.

### Reducing Bugs with Raygun, .NET Aspire, and Local AI

Presenter:

- John-Daniel Trask, Raygun co-founder and CEO

John-Daniel Demoed adding RayGun to a .NET App with .NET Aspire:

- Utilize `appsettings.json` to configure dev and prod versions of services with an API key.
- Not all RayGun features require an API Key.
- Use local LM to help with a .NET Aspire-infused Application.
- CHeck out the RayGun blog for information about how they integrated Ollama into .NET applications.

## Hands-on with MS Learn

Notes taken while following [MS Learn DotNet Aspire steps](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/build-your-first-aspire-app?pivots=vscode) using VS Code as the IDE.

### Docker Desktop

There is a prerequisite of installing Docker (Docker Desktop) to manage images for local and cloud deployment.

- Subscription service (although personal use, or business use up to a certain number of employees or income, is free of charge).
- Docker Desktop must be running to view, create, manage, and remove images.
- A registry system making locating pre-built Docker Images easier to find (and therefore a login account is required).

### Create New DotNet Aspire Application with VS Code

In the terminal, execute: `dotnet new aspire-starter -o target_directory`.

Using VS Code: Open the Command Palette and select ".NET Aspire Starter Application".

### Testing The Application Locally

It might be necessary to configure dotnet to trust the developer certificates by using `dotnet dev-certs https --trust`.

_Note_: I have not had to do this before, nor did I have to do it this time. It could be that since I've responded "Yes, trust this certificate" in the past within the browser view, this step is no longer required on my workstation profile.

To launch from the terminal: `dotnet run --project .\project_path\project_file.csproj` and view the Terminal output to get the URL and port(s) to plug-in to the browser.

The Aspire Resources page will have links to the Endpoints that can be clicked to launch a browser to view the endpoint WebApp.

### DotNet Aspire Starter Template Project Hierarchy

- ApiService: Asp.net Core Minimal API Project. Depends on AspireSample.ServiceDefaults project.
- AppHost: Orchestration project. Connects and confgures related projects and services. Set this as the Startup Project. Depends on ApiService and Web projects.
- ServiceDefaults: Shared configuration project, accessible by all solution projects. Enables Resilience, Service Discovery, and Telemetry.
- Web: Asp.net Core Blazor App. Has a _default_ Aspire configuration. Depends on ServiceDefaults project.

Project Definition - Aspire Host Project:

- `<IsAspireHost>true</IsAspireHost>`
- ItemGroup Project References identify to the supported sibling projects.
- ItemGroup Package references point to included packages like `Aspire.Hosting.AppHost` and `Aspire.Hosting.Redis`.

Project Definition - Service Defaults Project:

- `<IsAspireSharedProject>true</IsAspireSharedProject>`
- ItemGroup Framework Reference to `Microsoft.AspNetCore.App`.
- ItemGroup PackageReferences include many packages including (but not limited to) `Microsoft.Extensions.Http.Resilience`, `Microosft.Extensions.ServiceDiscovery`, and more.

File `Extensions.cs` exposes methods that enable additional behaviors and capabilities:

- `AddServiceDefaults()`: Extends `EHostApplicationBuilder` type. Additional extension functionality can be added as necessary!

### Add Aspire Orchestration to an Existing Project

_Note_: The following instructions are using the Cli. Using Visual Studio is much simpler and information is included below.

#### Using Cli Commands and DotNet

Add an App Host Project using DotNET Cli:

1. Add an Aspire AppHost project: `dotnet new aspire-apphost -o project_name`
2. Add the AppHost Project reference to the Solution file: `dotnet sln solution_file add path_to_project_file`
3. Add Project references to AppHost that point to other Projects it needs to know about: `dotnet add apphost_project_file reference other_project_file`

Add a Service Defaults Project:

1. `dotnet new aspire-servicedefaults -o eShopLite.ServiceDefaults`
2. Add the Service Defaults Project reference to the solution file: `dotnet sln solution_file add path_to_project_file`
3. Add Project reference to AppHost that points to the Service Defaults Project: `dotnet add apphost_project_file reference other_project_file`
4. Add Project references in other Projects that reference the Service Defaults project (enabling _service discovery_) (use dotnet cli commands for this, too).
5. Open `Program.cs` in each of the original Projects and add the line `builder.AddServiceDefaults()` immediately following `var builder = ...` line.

Update App Host Project:

Add the following lines to the AppHost project's `Program.cs` file after `var builder = ...`: `builder.AddProject<Projects.proj_name>("friendly-name");`, one for each Project to be added to the orchestrator.

Enable Service Discovery To Existing Projects:

1. Use _function chaining_ following `builder.AddProject<T>()` to add services to Service Discovery.
2. To Add http endpoints for deployment to a Cloud or Hosted environment: `.WithExternalHttpEndpoints()` (skipping this step will render the app inaccessible to external http clients).
3. To Add a reference to a dependency Project use `.WithReference(friendly_name)`
4. Update `appsettings.json` of the primary Project (application) to change the URLs to use the _friendly-name_ of the endpoints host (instead of `localhost`). This ensures Aspire can find the endpoints and also ensures the endpoint IDs are discoverable.

#### Using Visual Studio

Using Visual Studio to add .NET Aspire components and reference to an existing Solution is much simpler than doing so by the CLI.

Adding Orchestration Support:

- Right-click a project to enroll in Aspire and select "Add .NET Aspire Orchestrator Support".
- Aspire Configuration Defaults and Aspire AppHost Projects are added and configured _automatically_ via this right-click menu item.
- Subsequent uses of the same r-click command will ensure additional Projects are added to the newly created Aspire projects AppHost and ServiceDefaults. :tada:
- The Startup Project is reconfigured to be `AppHost` project added by Aspire. :smiley:

Adding Service Discovery:

- Open `Program.cs` in the AppHost project and add extension methods `.WithExternalHttpEndpoints()` and `.WithReference(friendly-name)`, referencing "store". This enables discovering the Store endpoint address to simplify deployment to local or cloud-based platforms.
- Update `appsettings.json` in the Store project to use a more generic "ProductEndpoint" and "ProductEndpointHttp" e.g. `http://products` and `https://products`, matching `friendly-name` configured above.

### About Dotnet Cli Versus Visual Studio

- Quick and easy `dotnet` commands help get up and running rapidly.
- Adding references using `dotnet` can be a bit challenging.
- Creating new Solutions and Projects take a bit of time and know-how using `dotnet`.
- Project and Solution creation are simplified using Visual Studio.
- Right-click options on Project files in Visual Studio add context-aware menu items for rapid Project updates like 'Add .NET Aspire Orchestrator Support'.
- Drag-and-drop can pay off by allowing Project File dragging to create a Project Reference quickly and easily.

## DotNET Aspire Tooling

Assist in creating and configuring cloud-native applications.

- Starter project templates.
- tbd...

## Aspire Limitations and Gotchas

As of 27-Sept-2024

- Aspire is delivered through the NuGet system, and Aspire _Workloads_ components are required and must be updated over time.
- DotNET 8 or newer is required, so any dotnet 7.x or older (LTS) framework projects will need to be updated first.

## Microservices and Aspire

.NET Foundation Presentation "Increase Observability, Resiliency, and Dev Usability with .NET Aspire".

Presenter: Lee Richardson

Aspire targets microservice-based projects, but can be used for non-microservice solutions, too.

Aspire brings together all of the resiliency features already in .NET 8+.

Aspire adds observability to the mix, allowing the ability to see bugs in apps, even if they are not noticable due to resiliency mechanisms auto-recovering.

- Azure Application Insights adds observability. Arguably too difficult and clumsy to use.
- Aspire Dashboard Resources page is in the box and allows drilling-down into the application interfaces and services.
- Structured Logs allows viewing transaction and session logging information including stack trace information.
- Traces shows events and timing for API calls such as REST and other WRRC.
- Metrics displays real-time graph and tabular data to view connection timings and spikes, memory usage, etc.

Problem Injectors for Scalability and Resiliency Testing:

- .NET Core 2+: Polly
- ChaosMonkey
- Resiliency Policies in .NET 8+: `AddStandardResilienceHandler()` applies basic policies that are customizable.

Strategies:

- Rate Limiting
- Total Timeout
- Retries
- Circuit Breakers
- Attempt Timeout

Open Telemetry:

- Brings consistent view and setup to get telemetry from applications and services.
- No longer have to rely on multiple SDKs and cobble together one or more solutions to gain Observability.
- Supports Logs, Metrics, and Traces (the 3 pillars of observability).
- Standardized protocol to provide observability.
- Aspire supports Open Telemetry out of the box.

Developer Usability of Aspire:

- Add service to the service DI container using AppBuilder and simply point to the named service.
  - Rather than having to configure 'http' and 'https' ports directly via configuration.
- Additional Services env-vars such as 'services__products__http__0' and 'services__products__https__0':
  - Supports Service Discovery is then just configured via JSON.
- Adding a new services (Aspire Integrations) simplify adding services like Redis.
- Integration with Docker enables automating download of Docker Images and running them by replacing 'docker-compose.yaml' files!
  - Requires additional Aspire Integration(s).

## Service Discovery

Setting `.WithReplicas(int)` in AppHost service discovery automates multi-instance deployment:

- WebApp: Requests are multiplexed to multiple HTTP instances at a single hostname.
- YARP is used behind the scenes to manage replica routing.

Setting `.WithReference(string)`:

- Use to ID a specific instance by its IConfiguration identification e.g. `https://localhost:7032`
- Use to ID a named instance using magic strings e.g. `web`
- Add/Update AppHost `AspireProjectResource` project setting to `false` and create a class that sets constant variables to name the instances.
- Add a service (e.g. Redis within a Container) for cache: `.WithReference("cache")` (will also need to set up redis with `services.AddOutputCache(options => {})`)
- Add an executable: `service.AddExecutable(string args)`

Add Consumers and Publishers using `builder.Services.Addnnnnn(string connName, params...)`:

- RabbitMQ
- Databases
- Cache (not just Redis)
- Etc

Setting `.WithManagementPlugin()` on a builder service add (see above) includes known plugins:

- Management
- Logging
- Tracing
- Heartbeat/health monitoring and response
- Example: Add RabbitMQ to AppHost and get it plugged-in to Aspire management and insights!

## Caveats Of Note

It is really easy to import a Docker/Podman container for services like Redis, however there are important implications and cloud-deployment considerations:

- Deploy to Kubernetes (or similar cloud container service) as a multi-container system.
- Deploy to Cloud services plus containers for only those services that need it (i.e. Blazor can be an AppService, SQL can be AzureSQL, and other services as containers).
- Deploy to Cloud services as native cloud services.
- Azure-Aspire package for Redis is a toolchain available for one or more of the above scenarios.

## Resources

- [.NET Aspire Workshop Repo on GitHub](https://github.com/dotnet-presentations/dotnet-aspire-workshop)
- [.NET Aspire and KeyCloak](https://aka.ms/aspire-keyvault)
- [jerrys demo project](https://github.com/jerrynixon/aspire-sqlserver)
- [MSFT resources for DAB](https://aka.ms/dab)
- [.NET Aspire Dev Day resources](https://aka.ms/dotnetAspireDevDay/Collection)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
