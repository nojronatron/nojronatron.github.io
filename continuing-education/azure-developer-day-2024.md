# Azure Developer .NET Day 2024 Notes

Multiple presenters, multiple presentations!

The following is a collection of notes taken _very rapidly_ while watching these sessions.

There will be missed information, misspellings, and maybe some incorrect information too.

## Table of Contents

- [Understanding Semantic Kernel](#understanding-semantic-kernel)
- [GitHub Copilot for SQL Development](#github-copilot-for-sql-development)
- [Azure Cache for Redis](#azure-cache-for-redis)
- [Event-Driven Architectures 101](#event-driven-architectures-101)
- [T-SQL for Cloud-Native Developers](#t-sql-for-cloud-native-developers)
- [Regex Support in Azure SQL Database](#regex-support-in-azure-sql-database)
- [Azure SQL DB Hyperscale and Named Replicas](#azure-sql-db-hyperscale-and-named-replicas)
- [Whats New in MongoDB for Azure and .NET](#whats-new-in-mongodb-for-azure-and-net)
- [Azure API Center](#azure-api-center)
- [Automated Web Testing With Playwright](#automated-web-testing-with-playwright)
- [Mastering the Dev Experience](#mastering-the-dev-experience)
- [References](#references)
- [Footer](#footer)

## Understanding Semantic Kernel

Bruno Capuano, .NET CA

Azure AI Studio:

- Deploy Chat GPT models at platforms to build on.
- _Local_ or Azure-based or OpenAI-based models can be developed against.

Built of Plugins with Prompts (plain text file) and Configurations (JSON).

Write Out Of Office messages from AI!

Combine prompts and configurations to create more advanced capabilities and responses.

Highlighted features:

- Automatic function calling
- Handlebars planner

aka.ms/ebskheroesrepo
devblogs.microsoft.com/semantic-kernel

## GitHub Copilot for SQL Development

Subhojit Basak, Product Manager, Azure Data.

"Integrate AI into regular DB Development"

- Use `--` prefix text to write a prompt and Copilot will add ghost-code for you to accept or refuse
- Copilot will also "guess" by ghost-writing `--` prefixed text. This can be accepted or rejected, too.
- Similar feel to how it works in VS Code and Visual Studio.
- Writing SQL Code is supportd in VS Code, VS 2022, JetBrains, and Azure Data Studio.

Copilot Chat is enabled, too.

Copilot is NOT the pilot _you_ are:

- Writing prompts for Copilot has a learning curve.
- Be aware that Copilot might end up changing context and generating different output.

## Azure Cache for Redis

Catherine Wang, Product Manager, MSFT

Stanley Small, MSFT

- Redis can be a multi-purpose Datastore for Intelligent Apps.
- Redis can cache the semantic queries for future requests: "semantic cache".

## Event-Driven Architectures 101

Davide Mauri, Principal Product Manager, Azure SQL, MSFT

Capture, communicate, process events between decoupled services. Common approach in modern Apps build with microservices.

- Events represent change in state or some updates.
- Event producers publish events to an event router.
- Event Router filters and pushes to event consumers.
- Event Consumers react to the event notifications.

Azure Functions:

- Event-driven
- serverless
- compute platform
- support most common lanugages + BYO Language
- Full on-prem support
- Triggers cause functions to run
- Trigger define how function is invoked
- Function must have exactly ONE trigger

Can an Azure Function be activated when data in a DB is changed? How can the change be detected efficiently? How to define the function that gets executed?

- The DB would become the Function Trigger!
- Azure SQL Change Tracking does this!
- Monitors Table to determine if/when data is changed.
- Detects which row(s) were effected.
- Change Tracking avialalbe in all Azure SQL services.

Azure Function SQL Trigger:

- Not a DB Trigger, but an Azure Function Trigger.
- Monitor one or more talbes for data changes.
- Executes an Azure Function when change is detected.
- Aggregate changes, batched changes, and pending changes: Concepts applied in AFSQL Trigger service.
- Only "latest" version of the row is available.
- Automatic rety: Connection error or exception recovery.
- Batch size, number of chagnes (per worker) and poling interval configuration options (default polling: 1 sec).

## T-SQL for Cloud-Native Developers

Presenter: Abhiman Tiwari, product Manager, MSFT

Why JSON:

- Enable transfer between disparate systems.
- Common data format across APIs.
- Application integration is simplified.

JSON Document Support:

- Azure SQL DB.
- SQL Server 2016 and 2022.
- Binary data (documents) are stered in queryable format.

## Regex Support in Azure SQL Database

Presenter: Abhiman Tiwari, Product Manager, MSFT

- Flixible pattern matching.
- Maninpulate query data.
- Improved data validation.
- Transform and standardize data.

RegEx Support:

- POSIX standardized.
- Case sensitivity, character classes, quantifiers, anchors, and capturing groups.
- More complex and powerful search patterns ar epossible.
- Currently in private preview across all tiers of Azure SQL DB.

New Functions:

- REGEXP_LIKE
- REGEXP_COUNT
- REGEXP_INSTR
- REGEXP_REPLACE
- REGEXP_SUBSTR

## Azure SQL DB Hyperscale and Named Replicas

Attinder Pal Singh, Product Manager, Azure SQL DB

HyperScale - Read Scale out:

- Compute, storage, and log service layers are distributed.
- Mitigates usual Scaling challenges.
- Compute can be scaled at a more fine-grained level, rather than with the entire SQL Scale container.
- Logs and other Storage grows seemlessly without impacting other components!
- Adding multiple compute nodes with Named Replicas is now a set of component-level "horizontal" scale-out operations.
- Same storage is still leveraged, therefore no additional storage provisioning costs.
- Log Services and Storage layers are accessed directly by/to the initial Compute and the Named Replicas.

Implement Named Replicas to act as the SQL DB for:

- Read or Read/Write Applications.
- Reporting services like PowreBI or Graphana.
- APIs.
- Limiting latency through shared storage and individual access per interfaces (as listed above).

Zone Resiliency:

- Create Named Replica in one zone.
- Add secondary replicas in other zones.
- Paging, data files, and snapshots are still shared by the Page Servers and Zone-redundant Storage layer.

Additional Named Replica Capabilities:

- License/Storage costs: Only pay for Compute!
- Monitoring: Portal metrics, Dynamic Management Views, and DB Watcher.
- Auditing: Inherits from primary R/W DB and logical server.
- Elastic Pool: Add Named Replica DB FOR Elastic Pool, but cannot be add IN Elastic Pool.
- Isolated Access: SQL/MSFT Entra Authetnciation, isolated compute and principals. Requires separate logical server to implement.
- Mix and Match: Service Level Objective, Hardware series, serverless/provisioned, and option of Zone Resiliency.

## Whats New in MongoDB for Azure and .NET

Luce Carter, MSFT MVP, Developer Advocate at MongoDB

MongoDB is:

- Document database, similar to Key-Value DB.
- Stores information in Collections of Documents.
- Is a general purpose DB.
- Flexible schema across Documents and Collections.
- Data validation options included.
- Horizontal Scaling is supported.

MongoDB is a platform for developers:

- The DB itself.
- Atlas Device SDKs.
- Charts (and graphs) that do not require additional development.
- Analytics, also supporting PowerBI.
- Search, based on Full Text Serach and Vector Search.

Why MongoDB instead of SQL DBs?

- Three-node based redundancy/fail over.
- Flexibility.
- Vertical Scaling.
- Horizontal Scaling (a.k.a. Sharding): Shares data across instances in Groups of Documents with a built-in lookup service.
- Readability: JSON-based format.

Why MongoDB Atlas instead of CosmosDB?

- Azure Marketplace includes Atlas pay-as-you-go Plan.

MSFT Semantic Kernel:

- Can be integrated with OpenAI and MongoDB Atlas.
- An Azure Connector connects Semantic Kernal with Mongo Atlas DB.
- Kernel Memory allows more than simple text search, extending Semantic Kernel and AI use cases.

MongoDB PRofvider for EF Core

- Will go GA soon.
- Similar Context setup, inheriting from DBContext and uses DBSets to define the data context.
- Attributes are used to map to MongoDB Collections: `[Collection="MyCollection"]`.
- Use string methods in Required and Display attributes to deteremine error messages, plain-english names, etc.
- Use `options.UseMongoDB(database name, connection string)` to setup the connection options.

## Azure API Center

Justin Yoo, Principal Cloud Advocate, Developer Relations, MSFT

"Are your APIs OK?"

Investments in APIs have and continue to increase, and most develpment efforts are put into working _with_ APIs.

Problems:

- API Sprawl.
- Visibility/Discoverability is not high, creating "shadow APIs".
- Fall out of compliance and not well documented.

API Inventory/Portfolio:

- Does not matter what _type_ each API is.
- Simply record and govern the existing APIs.
- Azure API Center aims to resolve these issues and become the Portfolio manager.

Azure API Center:

- Register all types of APIs (REST, etc).
- Manage lifecycle of the APIs (deprecated, retiring, active, etc).
- Document who owns the API, where the repository is, and what Compliance contract the API adheres to.

Build a Complete API Inventory:

- Register new APIs using Azure-CLI or import using Azure API Management.
- Add APIs that you don't directly manage, but want to keep a link to.

Under the covers, the feature is:

- JSON Data: API metadata is used to store API location(s), name, and other information.
- Service: Manage deployments, utilization, and lifecycle.
- Reporting: See graphs of usage and information about APIs.
- Ease of Management: Direct links to API sources (from metadata), etc.

Governing APIs:

- Track API Metadata.
- API Process Automation.
- Data conformance.
- Etc.

Discoverability and Consumability:

- Portals: API Center, WordPress Plugin, Backstage Plugin.
- GitHub, VS Code, VS 2022 developer tools.
- Copilots: Github Copilot, Copilot for Microsoft 365 to "shift left" management of these API services.

API Center Plug-in For Visual Studio/VS Code

- Copilot integration allows the expected interactions and code generation suggestions.

## Automated Web Testing With Playwright

Debbie O'Brien

Vansh Singh

About:

- Open source.
- Test modern web apps.
- All modern brwosers.
- JavaScript, Python, and .NET support.

Features:

- Codegen: Generates tests by clicking through the website. Assertions ('Expect') are generated while the test engineer walks through a test case in the UI.
- Trace Viewer: Full trace of tests, step-through step actions, see entwork and console, pop-out DOM snapshots for inspection, and more. Allows viewing elements with the "Locator" embedded tool.
- Auto Waits: Waits for checks to pass before performing actions.
- Tests in Paralell.
- Auto-Retry assertions.

Microsoft Playwright Testing (MPT): Run tests at-scale with browsers in the cloud.

- Extends Playwright framework.
- Expedites test runs and build pipelines using parallel tests against cloud-hosted browsers.
- Run test suite fatser on local workstation.
- Improve test coverage.

## Mastering the Dev Experience

Dev Productivity Dojo: Master Project Setups Using VS Code!

Ori Bar-ilan, Sr. Software Dev Engeneer at MSFT Education (.NET, Python, VSCode, Azure).

Mermaid: Charting software has VSCode Extensions. Use markdown to define charts, check them in to your repo!

Command Runners to Review:

- JUST
- TASK

Code Formatters:

- CSharpier: Prettier for C#. Opinionated code formatter with limited configuration/control.

Using TODO Comments:

- Great for local work.
- _Bad_ for checking in to code.
- Lint this out using a tool like `todo-tree`.
- VSCode Workspace Settings can also be set to ignore checking-in TODOs.

## References

- [Azure Developer Hub](developer.microsoft.com/azure).
- [Agenda](aka.ms/azuredevelopers/dotnetday).
- [Session Links](aka.ms/azuredev/dotnetday/learnmore).
- [Cloud Challenge](aka.ms/azuredevelopers/dotnetday/challenge).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
