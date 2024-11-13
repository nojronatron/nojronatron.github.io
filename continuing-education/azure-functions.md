# About Azure Functions

This document was created to store learnings about Azure Functions.

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

aka.ms/aspire-functions-

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

Functions can also be created "on the fly" instead of with the Command Palette.

- Follow Intellisense advice to drive development.

_Note_: AzureWebJobsStorage configuration item must be set properly for Storage Emulator service to work locally.

Gavin's second demo showed what amounts to a minimal API with CRUD capability using decorated Python code pushed to Azure Functions.

#### Decorators Add The Magic

Azure Functions are just plain Python functions, but the _Decorators_ in Python tell Azure the Function should be run in the Azure Functions service!

## References

Azure Functions [V2 Python Programming Model](https://techcommunity.microsoft.com/t5/azure-compute-blog/azure-functions-v2-python-programming-model)

Azure Functions [Python Developer Guide](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-python)

Quickstart: [Create JavaScript function in Azure using VS Code](https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-node)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
