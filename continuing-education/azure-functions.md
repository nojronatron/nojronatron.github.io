# About Azure Functions

This document was created to store learnings about Azure Functions.

## Table of Contents

- [Azure Functions Basics](#azure-functions-basics)
- [What About Logic Apps?](#what-about-logic-apps)
- [What About WebJobs?](#what-about-webjobs)
- [Develop Azure Functions](#develop-azure-functions)
- [Azure Function Development Requirements](#azure-function-development-requirements)
- [DotNET Conf 2024 Azure Functions in DotNET 9](#dotnet-conf-2024-azure-functions-in-dotnet-9)
- [Azure Friday Develop Azure Functions Using V2 For Python](#azure-friday-develop-azure-functions-using-v2-for-python)
- [References](#references)
- [Footer](#footer)

## Azure Functions Basics

- [x] Explain what are Azure Functions and the base features.
- [x] Describe when it is best to use Azure Functions over other frameworks or App-like systems.
- [x] Overview the pricing structure of Azure Functions.

### Azure Function Feature Overview

- Support for C#, Java, JS, PowerShell, and Python.
- "Custom Handler" allows using other languages.
- Automation.
- Functions have tooling for development and debugging.
- "Consumption" plan or "Premium" and "App Service" plans.
- Securely utilize Environment Variables to enable authenticated Function interactions.

### Azure Functions Are

- Cloud-based compute service.
- Event-driven.
- Scalable serverless compute.
- Event-driven: Either external events or scheduled (CRON or timer).
- PaaS (Platform As A Service).

### Azure Function Triggers

- Start the execution of your code.
- Process inputs.
- Pass processed data to your Functions.
- Listen to other services like storage e.g. Azure Cosmos DB when a row is inserted.
- Azure Event Grid triggers.
- Web requests or Web Hooks.
- Azure Queue message.

### Azure Function Bindings

- Code you don't have to write.
- Connect Function code to services.
- Connect your Function with Azure Services using Bindings.
- Input Bindings: Provide input _to_ your Function, _from_ a data source (might or might not be same as Function Trigger).
- Output Bindings: Write data to destinations.

### Plans

- Consumption: Pay-per-running-time. Automatic scaling. Good for intermittent, short-process workloads. Includes some startup delay/not instantaneously executed. Limited execution time.
- Premium: Functions always initialized, so no startup delay. Long running Functions with dynamic scaling. Execution time extensions vs. Consumption plan.
- Dedicated: Tied to an App Service Plan. Best for continuous-run Functions.

#### Consumption Plan

Defaults and Maximums:

- 5 minutes to 10 minutes.
- Windows: 200 instances.
- Linux: 100 instances.

#### Flex Consumption Plan

Offers:

- High scalability compute choices.
- Virtual networking.
- Pay-as-you-go billing.

Defaults and Maximums:

- _Code only_ Linux hosted, Windows Deployment _not_ supported.
- 30 minutes to unlimited.
- Instances limited by collective memory usage across a Region.

#### Premium Plan

Good for:

- Run continuously (or nearly).
- Enable event-driven scaling.
- Collect Functions into the same scaling plan.
- Low GB seconds utilization.
- More CPU provisioned.
- Virtual network connectivity.
- BYO custom Linux image!

Defaults and Maximums:

- 30 minutes to unlimited.
- Windows: 100 instances.
- Linux: 20-100 instances (depends on region).

#### Dedicated Plan

Consider for these situations:

- Fully predictable billing.
- Manual scaling is required.
- Multiple WebApps and Function Apps within the same plan.
- Larger compute sizes needed.
- Fully isolated compute.
- Secured entwork access using App Service Environemnt (ASE).
- High memory usage and high scaling are necessary.

Defaults and Maximums:

- 30 minutes to unlimited.
- 10-30 instances, or up to 100 using ASE.

### Scaling Function Apps

Function App: The context within which Azure Functions are executed.

- Share same settings and connections.
- Single unit of deployment and management.
- Scaled by adding more Function App instances (Premium and Consumption plans).
- Resources shared and scaled at the same time.

### Monitoring Functions

Azure Application Insights:

- Logs
- Performance statistics
- Error data
- Built-in to Azure Functions
- Traces

_Note_: Azure Application Insights is not enabled by default, but if the Function project was creating using the Azure Functions Extention, the code to enable is simply commented-out in Program.cs.

### Function Components

- Function Triggers: Cause Function to execute. Defines invokation. Limited to a single trigger.
- Function Bindings: Declarative connection to another resoruce. Can be input, output, or both. Can use Client SDK instead of Bindings as an alternative.
- Function Runtime: Many available including .NET Core, Node.js, Java, PowerShell, and Python. Functions RunTime can be loaded and executed in a local Dev Environment.
- API Management (APIM): Security and routing for HTTP-triggered Functions. Endpoint is exposed as REST API.
- Deployment Slots: Each Slot is a separate instance. Slots are exposed to a publicly available endpoint. Useful for versioning and upgrading Functions.
- Function App Configuration: Connection String. Env Vars. App Settings. All defined separately for each Function App. Read-in these variables as "Enviornment Variables" in the Function code.

### When To Use Azure Functions

Event-based applications:

- Reminders and notifications.
- Scheduled Tasks.
- Experimental APIs and Scalable Web APIs.
- Irregular Workflows.
- Queuing processable work.
- IoT Stream Analysis.
- Process File Uploads (screen inbound Blob-store data).
- Process data _in real time_.
- Serverless Workflows: Chain Azure Functions and introduce State to create Durable Functions to monitor external events, perform branching logic, and invoke other Functions.
- Integrate with AI to "infer on data models" for analysis and classification.
- Respond to database changes such as document creation or change in Azure Cosmos DB.
- Develop reliable messaging systems e.g. Process message queues using Queue Storage, Service Bus, or Event Hub.

### Hosting Options

Functions are hosted on either Windows or Linux environments. Containers (Docker?) are supported as follows:

- Consumption plan and Flex Consumption plan: No containers.
- Premium Plan, Dedicated Plan, and Container Apps: Linux.

The type of platform and whether or not to use a Container will impact how the Function is scaled, resources ultimately available to the Function, and support for advanced functinoality including Virtual Network connectivity (or not).

### When To Use Container Apps

- Fully manage environment.
- Leverage Functions programming model to build event-driven, cloud-native function apps.
- Run alongside other microservices, APIs, Websites, and Workflows.

Defaults and Maximums:

- 30 minutes to unlimited.
- 10-300 instances.

## What About Logic Apps?

Also a serverless workload service:

- Is a Workflow Integration Platform.
- Create complex orchestrations.
- Built using a GUI or editing configuration files.
- Design-first (declarative).
- Large-connection types catalog including Enterprise B2B scenarios.
- Ready-made actions library.
- Monitor using Azure Portal and Azure Monitor logs.
- Manage using Azure Portal, REST API, PowerShell, or Visual Studio.
- Execute in Azure, locally, or on premises.

Azure Functions:

- Are pure code.
- Can do workflow integration by using the Durable Functions Extension.
- Code-first (imperative).
- Few built-in connection/bindings types.
- One Function per "Activity".
- Monitored using Application Insights (not enabled by default).
- Manage using REST API and Visual Studio.
- Execute in Azure or locally.

## What About WebJobs?

Similar to Azure Functions and:

- Code-first integration service.
- Aimed at developers.
- Built on Azure App Service.
- Source control integration.
- Authentication.
- Monitoring.
- Application Insights.
- Fewer overal features than Functions.
- Most trigger events like Functions: Timer, Queues, Service Buss, Blobs, Topics, Cosmos DB, Event Hubs, File System.

Azure Functions:

- Serverless app model.
- Automatic scaling.
- Dev and test in browser.
- Pay-per-use pricing.
- Integration with Logic Apps.
- Many trigger events including: Timer, Queues, Service Bus, Blobs, Topcis, Cosmos DB, Event Hubs, HTTP/WebHooks, Event Grid.

Overall, Azure Functions provides more for developers including:

- More programming language support.
- More dev environments.
- Azure Service integration.
- Pricing.

MSFT says Functions are usually a better choice than WebJobs.

## Develop Azure Functions

Concepts:

- [x] Describe key components of Functions: Bindings and Triggers.
- [x] Create triggers and bindings: Use VSCode and Command Palette to get started.
- [x] Describe how to control when a Function runs and where its output is directed: A Trigger defines when a function runs, and output is directed according to its Binding.
- [x] Summarize how to connect Functions to Azure Services: Decorate strongly-typed language Properties and Methods with Attriubutes, and use `function.json` schema to define bindings for script-y languages including JS and TS.
- [x] List steps to create Functions in VS Code and Azure Functions Core Tools: See [Development Steps](#development-steps).

### Developing Functions Overview

Function App definition: Composition of one or more FUnctions, managed and deployed and scaled together.

- Same pricing plan.
- Same deployment method.
- Same Runtime version :arrow_right: _same language_ required in v2.0.
- Organizes a collection of manageable Functions.

Create and Test Functions Locally:

- Local dev environment has a Functions project directory.
- `host.json`: Configuration options applied to _all_ Functions in a Function App instance.
- `local.settings.json`: App settings and local deployment tool settings for the _local_ dev-test-run environment only. Be sure to _gitignore_ this file as it may contain secrets.
- Application Settings: Same as local.settings but applies to Azure Deployment settings.
- Other files depending on language and Function context and usage.

Azure-deployed Function App settings can be downloaded for sync to the local Function App instance.

### Triggers and Bindings

Triggers:

- Define _how_ Functions are invoked.
- May contain associated data, often provided as the payload of the Function.
- Each Function must have exactly one trigger.

Bindings:

- Optional.
- Declaratively connect with another _resource_ or _Function_.
- Input Bindings: Zero, one, or multiple.
- Output Bindings: Zero, one, or multiple.
- Input and Output Bindings.
- Bindings become Function _parameters_.
- Mix and match different bindings is allowed.

Benefits:

- Avoid hard-coding service connections.

### Defining Triggers and Bindings

Depends on language in use:

- C# ClassLib: Decorate methods and parameters with Attributes.
- Java: Decorate methods and paraemters with Annotations.
- JS/PoSH/Python/TS: Defined in `function.json` schema file.

Function.Json Schema:

- Use the Portal UI to add bindings from the Integration tab.
- Edit the file directly in the Portal UI from the Code + Test tab.

_Note_: Portal-defined Triggers and Bindings in C# actually use `C#Script` which necessetates using `function.json` schema file.

DataTypes:

- For strongly-typed languages.
- Set using `dataType` parameter in JSON.
- `binary`, `stream`, or `string`.

Binding Direction:

- Triggers: Always IN.
- Input, Output: In, and OUT, respectively.
- Special: `inout` is reserved for certain binding scenarios.
- For typed languages: Provide this in an attribute constructor.

Example C# Attributes:

- `[FunctionName(<string>)]`
- `[return: <type>(string name, Connection = string secret)]`

Function Definition in C# Method:

- Define a class that represents the Function return type. Static or instance-classes are acceptable.
- Define a Method to represent the Function. Can be `static` or an instance method.
- Identify the Function return type in the static method.
- Apply the Attributes to define the Function Name and Function Return type.

### Connecting to Azure Services

- Use Application Settings functionality of Azure App Service for secure configuration.
- Name-Value pairs are used to identify configuration items so secrets can be stored securely.
- Set the Application Setting _Name_ to configure the secret for the Trigger and Binding that require a connection Property.
- Similar to how DB Connection Strings are implemented in conjunction with Secrets and EnvVars in modern dev.

Optional: Azure Function may require an _Identity_ instead of a secret.

_Note_: Azure Static WebApps can **automatically** attach the Azure Functions. See [Azure Static Webapps, API Options](./azure-static-webapps-api-options.html) for details.

### Identity Based Connections

File services usually require authorization before reading and especially writing to them.

- For Consumption or Elastic Premium plan: Use `WEBSITE_AZUREFILESCONNECTIONSTRING` and `WEBSITE_CONTENTSHARE` parameters for accessing Azure Files.
- Azure Files does _not_ support Managed Identities to grant access.
- System-assigned ID or user-assign ID can be used as a Managed ID for other services.
- System and User IDs map to `credential` and `clientID` properties.
- UserID-to-ResourceID mapping _is not supported_.
- In local development, customization of the User-assigned ID is allowed.

Permission must be granted to the Identity:

- Assign a role in Azure RBAC.
- Specifiy the ID in an Azure Access Policy on the service that will be accessed.

### Development Steps

1. Meet [Azure Function Development Requirements](#azure-function-development-requirements)
1. Create New AzureFunctions project. An option is to use the Command Palette.
1. Select Language.
1. Select Runtime.
1. Select template: HTTP Trigger (other options).
1. Provide a Function Name.
1. Provide a Namespace for the function e.g. `My.Function`.
1. Select Authorization Level (anonymous, others...).
1. Develop and Debug the app locally.
1. Deploy the Function to Azure using Command Palette: "Azure Functions: Deploy to Function App..." and follow the steps.
1. Run the Function in Azure by opening the Azure Extension in VS Code then expand Resources, Function App, (Function ID), Functions, and the command e.g. "HttpExample".
1. R-Click the Function Command and select "Execute Function Now...", enter the Request Body, and view the output to confirm the Function App is working as expected.

### Interacting With Local Dev

While running in Debug Mode:

1. Activate the Function by opening the Azure Extensions icon.
1. Expand Workspace and select Local Development to see the Function.
1. R-Click and select "Execute Function Now..." to get a prompt for input in the Command Palette.
1. Enter a Name-Value pair in the Command Palette.

The Function executes, displaying output via Azure Functions Core Tools to the Terminal window.

## Azure Function Development Requirements

- Azure Account with an active subscription.
- Azure Functions Core Tools v.4.x or newer.
- VS Code on a supported platform.
- DotNET 8.x or newer.
- Azure Functions Extension for VS Code.

## DotNET Conf 2024 Azure Functions in DotNET 9

Presenters:

- Safia Abdalla
- Matthew Henderson

> Events handled by code.

Benefits of Azure Functions:

- Only write the code that is absolutely necessary.
- Stick with business logic.
- Not much configuration setup necessary.

Demo:

- Start with an Aspire Solution.
- .NET Aspire provides templates and packages to help build and deploy observable, production ready, cloud-based apps.
- Functions Project: Select "HTTP Trigger" project property.
- Scaffold-out an HTTP Function.
- Add necessary references such as 'Aspire Azure Storage Blobs'.
- Inject Aspire Service Defaults and any other packages like AzureStorage into the Functions Project DI (see Aspire setup and use instructions for details).
  - Remember to include `WithReference('refname')` to get Aspire Registration completed.

CSharp DevKit:

- Supports building and debugging Azure Functions in VS Code!
- Use 'Request.http' file to test WRRCs.
- Local debugging functionality across triggers and WRRC!

Benefits of Aspire:

- Structured Logs: View Invocation IDs to find WRRC pipeline events.
- Drill-down into events to get more information on success, errors, and time to process.

Build and Deploy to Azure:

- Certain triggers might have dependencies in order to execute or perform their roles.
- Adding Roles: Use BICEP, or the AZD/Azure Portal to set them, or use Aspire to register the Azure Function Project.
  - Pass-in custom Azure service Resource(s) in DI using Builder.
  - Configure other infrastructure role(s) in DI using Builder.
- Once configured, use `azd up` to publish to Azure.
- Azure Aspire Dashboard gets deployed into Azure too!

## Azure Friday: Develop Azure Functions Using V2 For Python

Host: Scott Hanselman
Presenter: Gavin Aguiar
Presenter: Shreya Batra

### Overview

Azure Functions:

- Event-driven Service
- Monitoring built-in!

Common Azure Function Use-Cases:

- Automation of Scheduled Tasks (supports Chron Jobs)
- DB Cleansing
- Data Deduplication
- Real-time Stream Processing

### Features of V2 Model

Fewer files, more intuitive Python development experience with Decorators, etc.

Integrated programming model:

- Triggers
- Input Binding: Additional data to use within the function
- Output Binding: Data to inject AFTER the function runs
- Simplified File System Model: One File captures all functions
- Templated Code within VS Code

Bindings are like Params and Return values, but for Cloud-based Functions.

_Note_: Other languages are available like JavaScript, C#, and more!

### Demo and Example Notes

How to create a function using V2 Programming Model?

1. VS Code with a new project folder.
1. Open Command Pallette => Create Function
1. Select Python (New Programming Model) (this creates a Virtualized Python Dev environment)
1. Review `getting_started.md`
1. Code is _generated_ as a sample that the developer can edit and take forward.
1. Open a Terminal and run `func host start`

Functions can also be created "on the fly" instead of with the Command Palette:

- Follow Intellisense advice to drive development.

_Note_: AzureWebJobsStorage configuration item must be set properly for Storage Emulator service to work locally.

Gavin's second demo showed what amounts to a minimal API with CRUD capability using decorated Python code pushed to Azure Functions.

#### Decorators Add The Magic

Azure Functions are just plain Python functions, but the _Decorators_ in Python tell Azure the Function should be run in the Azure Functions service!

## References

- [Azure Function Core Tools](https://github.com/Azure/azure-functions-core-tools)
- [Code and Test Azure Functions Locally](https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local)
- [Azure Functions Overview](https://learn.microsoft.com/en-us/azure/azure-functions/functions-overview?pivots=programming-language-csharp)
- [App Service Plan Limits](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#app-service-limits)
- Azure Functions [V2 Python Programming Model](https://techcommunity.microsoft.com/t5/azure-compute-blog/azure-functions-v2-python-programming-model)
- Azure Functions [Python Developer Guide](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-python)
- Quickstart: [Create JavaScript function in Azure using VS Code](https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-node)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
