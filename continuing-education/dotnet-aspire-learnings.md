# DotNET Aspire Learnings

Notes from my learnings about this MSFT Framework for .NET 8 and newer.

## Table of Contents

- [DotNET Aspire Developers Day](#dotnet-aspire-developers-day)
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
- Easy to build: Service discovere, developer dashboard, logs, metrics, distributed traces by adding an Aspire project.
- Easy to deploy: Single command run, App topology in C#, Cloud deployment support.

Aspire supports other language projects too!

Add Aspire To An App Overview

1. Have an existing app.
2. Add an Aspire AppHost project.
3. The Aspire Project creates an interface that provides logging, tracing, and various other features to help manage the existing app project(s).

Obviously, there's a bit more to it, but the above is the general idea.

_Announcement_: .NET Aspire 8.1 officially released 23-July-2024

### Enhance Business Processes with .NET Aspirea nd Generative AI

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

Problems Aspire Exists To Fix:

- Not easy to build distributed apps: Many components and configurations, caching and DB connection issues, etc.
- Resiliency and telemetry are complex but necessary for a production system.
- Reinventing the wheel, or just writing the same code and using the same system over and over again?
- Docker containers with many moving parts, or multiple containers to assemble a system.

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

- App composition: Specify projects, containers, executables, and clous resources that make up the application.
- Service discovery and connection strin gmanagement simplify service setup, configuration, and management.

Core Concepts:

- App Host: Central Project. All orchestration and service registration happens here.
- Starter App: Your project!
- Service Defaults: .NET Aspire project configurations.

Prerequisites:

- .NET 8.0+
- Aspire Workload
- OCI compliant container runtime (Docker Desktop or Podman)
- IDE like VS or VS Cdoe with C# Dev Kit Extension

Scaffold your Project:

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

## Resources

- [.NET Aspire and KeyCloak](https://aka.ms/aspire-keyvault)
- [jerrys demo project](https://github.com/jerrynixon/aspire-sqlserver)
- [MSFT resources for DAB](https://aka.ms/dab)
- [.NET Aspire Dev Day resources](https://aka.ms/dotnetAspireDevDay/Collection).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
