# MSBuild 2024 Notes

Microsoft Build is a yearly conference aimed at .NET developers and focuses on Visual Studio, languages like C#, F#, and Visual Basic, developing solutions using Azure or Microsoft 365, and updated information on .NET.

MSBuild takes place on 21 May through 23 May, 2024.

## Table of Contents

- [Level Up With DevBox](#level-up-with-devbox)
- [AI Safety and Security Fundamentals](#ai-safety-and-security-fundamentals)
- [Enterprise Class NGINX Plus Without Operational Toil](#enterprise-class-nginx-plus-without-operational-toil)
- [Scott and Mark Learn AI](#scott-and-mark-learn-ai)
- [.NET Aspire Dev On Any OS with VS Family](#net-aspire-dev-on-any-os-with-vs-family)
- [Demystify Cloud-Native Development with .NET Aspire](#demystify-cloud-native-development-with-net-aspire)
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

## Level Up With DevBox

Presenter: Scott Hanselman

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
- Polyglot Notebooks: Like Jypiter Notebooks, but allows `C#`, PowerShell, Python, etc.
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

Leslie interviewed Brian Ehlert, Director, Product Management, F5 NGINX.

General Notes:

- NGINX is _more_ than just a web server: Cache, reverse proxy, streaming server, etc.
- Clustering and state sharing: Client connection state is shared within the cluster with features like rate limiting.
- NGINX as a Service, 1st class service on Azure.
- NGINX+ unlock developer capabilities as a managed service, in L4 and L7 (which other services do not provide).
- Header and Body manipulation are possible, as well as authentication and session handling.
- More about [NGINX as a service on Azure](aka.ms/Build24FP/F5).

## Scott and Mark Learn AI

Presenters:

- Scott Hanselman, VP Developer Community "Programmer"
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

The other finalist was a team that developed hardware to detect emissions in metal fabrication plants, integrated with AI. Great idea for sure, and I wish that team well.

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

[DotNET Aspire GA Announcement](https://devblogs.microsoft.com/dotnet/dotnet-aspire-general-availability/).

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
