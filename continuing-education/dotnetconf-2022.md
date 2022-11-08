# DotNET Conf Notes November 2022

## Index

[The State of DotNET MAUI](#the-state-of-dotnet-maui)

[Container Apps](#container-apps)

[Azure Functions in DotNET](#azure-functions-in-dotnet)

## The State of DotNET MAUI

MAUI for DotNET 7 is now GA!

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

- Foldable device support (*.AndoroidX.Window)
- Window Positioning
- Tool Tips
- Context Menus
- Accessibility Improvements

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

Event-driven, serverless compute service. *[MSFT, DotNET Conference]*

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

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
