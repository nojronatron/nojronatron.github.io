# About Azure Functions

This document was created to store learnings about Azure Functions.

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
