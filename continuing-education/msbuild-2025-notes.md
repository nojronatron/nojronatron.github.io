# MS Build 2025 Notes

## Table of Contents

- [Keynote](#keynote)
- [Definitions](#definitions)
- [References](#references)
- [Footer](#footer)

## Keynote

Satya Nadella

Focus: **Open Agentic Web At Scale**

- Developer tools are used to tame complexity while creating solutions
- aka.ms/GitHubStories
- aka.ms/BookOfNews
- New cross-platform debugger
- VSCode: Open-source Copilot
- aka.ms/AgenticDevOps
- Azure SRE Agent: Triage, root-cause analysis, attempts resolutions
- Coding Agent now available: "Peer programmer" can be assigned tasks, generate docs, and author tests. Assign GitHub Tasks to Coding Agent. Generates and uses GitHub Actions, drafts PRs, and respects security measures, only uses it's own branch
- "Building a Secure and Open Ecosytem"
- OpenAI convo with Sam Altman
- Microsoft 365 Copilot: Chat, Search, **Notebooks**, Agents, etc all tied together. Grounded in web data and your own data.
- Special Agents: Researcher, Analyst, etc can all be used within Teams
- aka.ms/TeamsAILibrary
- aka.ms/ThirdPartyAgents
- Copilot Studio components: UI Automation (more, see the next link)
- aka.ms/MultiAgentOrchestration
- M365CopilotStories
- Enterprise Class Agents: **Copilot Tuning**. Learns company language and tone, expertise, etc through an initial training run and fine-tuning controls.
- aka.ms/CopilotTuning

Demo: Miti Joshi, Prin Prod Mgr, Power Apps

- Researcher Agent: Uses business data, built on OpenAI o3 "reasoning model". Will use citations to support its responses. Can scaffold code right in your project.
- Minimal-code Agents: Build your own Agent with very little coding. Provide instructions for the Response Agent, add Tools and definitions to enable triggering when to run and what workflow(?) or tool (MCP servers, 3rd party services, etc) to execute.
- Multi-Agent Orchestration: Agents collaborate with each other to take on more complex tasks.
- Compliance tool checks for AI settings not meet requirements.
- Task Types are targeted for generation such as Document (for a contract).

Back to Satya:

- MCP Services and Agents coming together to improve and simplify complex tasks.
- Apps and Agents: Build your own apps and extensions
- AI Platform: Regular releases of production-ready with samples that are multi-model and multi-agent
- Azure AI Foundry: Complete platform "for the AI Age"
- aka.ms/FoundryStories
- Foundry can work with many common AI models
- aka.ms/ModelRouter
- Grok (xAI) soon to be available in Azure
- Recorded interview with Elon Musk
- aka.ms/FoundryModels
- More OLlama (Meta) models coming to Azure
- Additional HuggingFace models coming to Azure
- Foundry Agent Service now GA
- aka.ms/FoundryAgentService
- aka.ms/AIAppPlatform
- BYO Models to Copilot Studio
- aka.ms/FoundryCopilotStudio
- Video: Stanford Medicine using Healthcare Agent Orchestrator
- aka.ms/Stanford
- aka.ms/HealthcareAgentOrchestrator
- aka.ms/FoundryObservability
- EntraID Agents: Enabled within Copilot Studio
- aka.ms/EntraAgentID
- aka.ms/SecurityForAI
- Defender integrates with Foundry

Demo by: Kedasha Kerr, Dev Advocate, GitHub

- AI Travel Agents assist with planning trips
- Grounded Responses using Azure AI Foundry
- Copilot-generated PR can take PR Conversation Feedback and perform work on the code to make changes, following coding standards and style
- Issues assigned to GitHub Copilot in GitHub Repo will get worked on asynchronously

Back to Satya:

- "Bring the power of app server and app building to the developer"
- aka.ms/FoundryLocal
- Agents as a Service, supported on Windows and Mac
- "Windows is the most open platform"
- On-device AI capabilities are increasing especialy through 3rd party services and apps
- aka.ms/WindowsAIFoundry
- Extends platform to support the full dev lifecycle including local and cloud
- Foundry Local is built into Azure AI Foundry
- LoRA for Phi Silica: Low-Rank Adaptation for LLMs and ML to fine-tune pre-trained models without updating parameters
- Native support for MCP in Windows including servers for settings, registry, and more
- aka.ms/MCPOnWindows

Demo: Divya Venkataramu, Dir Product Marketing

- Tools: VSCode, Copilot, MCP on Windows, VSCode, Figma, Windows Subsystem for Linux
- Multi-step prompts like: Get latest WSL image and build a website that does x
- Can review a Figma design, and use MCP to pull details from the correct source, and Copilot can generate the code per the Figma design and the user prompt requirements

Back to Satya:

- WSL is not fully open-sourced (Issue #1)
- aka.ms/WSLOpenSource

Demo/Chat: Kevin Scott, CTO, EVP of AI

- Agentic Web progress: Happening in an open way
- What is an Agent? A thing that humans can delegate tasks to
- Current Agents: Copilot, MS 365 Copilot, Researcher, Analyst, ChatGPT, and GitHub Copilot
- Protocols: MCP, ASA, etc.
- The Runtime Layer: "[An] Emerging set of components [Microsoft] is building"
- "Capability overhang": MSFT feels like the ability of Agents is beyond how they are being used today, to the tune of 12+ months of advance
- Azure Foundry will be a focus for the next few years
- Enabling Agents to take actions on your behalf require protocols to connect Agents to content and services to complete the delegated work
- MCP Support: 1st party, For enterprise and __ apps, supporting an open community
- There is a push to ensure ubiquity to support a standardized way to approach Agentic services (currently the hope is MCP is just this)
- github.com/microsoft/NLWeb
- NLWeb helps make a website or API an Agentic App using LLMs. Is an MCP Server

Back to Satya:

- Content and Intelligence can be more distributed and accessible
- Democratisation aggregation of intelligence
- Data: Any AI app relies on the data tier
- aka.ms/DataStories
- Video: NFL uses AI to evaluate data during "Combine", using Agentic tools
- aka.ms/NFL
- aka.ms/FoundryDatabricks
- aka.ms/PostgreSQLGenAI
- aka.ms/FabricDigitalTwin
- aka.ms/AIReadyOneLake
- aka.ms/FabricChatWithYourData
- Infrastructure: How to optimize performance and low latency and lowered cost and improved monetization
- AI Performance = Tokens / (Watt + $)
- Azure now has NVidia GB200 v6 GPUs available
- Video of Satya chatting-up Jensen Huang (nVidia)
- aka.ms/BuildNVidia
- Future: Hope to make Azure the largest supercomputer in modern times
- Azure has opened 10 new DC's around the world to support AI workloads
- Using closed-loop cooling to reduce water utilization
- AI WAN: 400 Tb/s backbone
- aka.ms/MetOfficeUK
- Video overviewing what Met Office UK does in Exeter, UK to analyze and forecast weather, using AI and Azure
- Digital Resilience: Data residency, confidential computing, and responsibel operations. Users maintain complete control
- Distributed AI Infrastructure: Azure Local
- Science: The domain that helps drive and accelerate new discoveries and effeciencies
- aka.ms/Science
- Announcement: Microsoft Discovery with Graph RAG (and more) to accelerate discovery

Demo John, Principal Program Manager, Product Innovation

- Use Microsoft Discover to help accelerate the scientific process
- PFAS (forever chemicals) are commonly used for Data Centers, this could be changed
- Research, Summary and Comprehensive reports, Citations to trusted research, generate hypotheses, plans to model plans to test hypotheses and findings validations, experimentation executes plan(s), results analysis and validation
- MSFT did research on immersion cooling without using PFAS using Microsoft Discover

Back to Satya

- Developer Tools
- aka.ms/BuildWithAI
- aka.ms/CopilotEducation
- MSFT has found Copilot to be an effective, positively impacting education intervention
- Video: Imlementing Copilot to assist providing quality education to children in Peru

## Day Two Keynote

Intro: Seth Juarez

Presenter: Jay Parikh, Ex VP MSFT CoreAI

- Has built infrastructure and tools for developers
- Principles: Use AI-driven platforms, transform entire dev exerpeince, embrace openness and choice
- AI-Powered Tools and Agent Factory
- Trust + Security are highlighted tenants
- Cloud-to-Endpoint context
- Added focus on burning-down technical debt
- Github Copilot is the "Immersive Experience" AI
  - Open PRs
  - Create README files with context and setup instructions
  - Perform work on behalf of the operator

Demo: Jessica Deen, Dev Advocate, GitHub

- Delegate work to Copilot Coding Agent, using the Assignees tool in Github
- Copilot Coding Agent "Next-edit Suggestions" adds AI and capability to Completions
- Copilot Coding Agent can be Chatted to help complete working through a GH Issue
- MCP powers Copilot Coding Agent through added contexts and tools like the ability to look at Figma files
- Copilot Coding Agent can also complete Commit Comments
- Copilot Coding Agent can help produce Mermaid diagrams from within Github Issue and PR workflows
- Github Models used by Copilot CA are available using Azure Model Foundry
- Azure SRE Agent records and addresses issues, recording activities (logs), and doing all the things we expect Copilot to do (talking through the issue and surmising a solution).
  - Will handle roll-back or other fix types
  - No person was involved in issue identification and resolution
  - An engineer can review the documents within a few minutes and be up to date on the cause and (short term) resolution
- Copilot Coding Agent can also help with upgrading SDKs, code platform, frameworks, etc

Back to Jay:

- Copilot: Plan, Execute, and Summarize
  - Update Java, .NET, etc
- Copilot will also help document existing code, provide unit tests, etc
- Copilot Coding Agent: Not available yet, will be released later this year
- Copilot cycle: Plan, Create, Operate
- MSFT has Integrated Anthropic "Cloud Code" into the GitHub Platform
- Video: Cathay Pacific uses Github Copilot Agent Mode
- Agent Factory: Foundry
  - MSFT is using Foundry in Copilot and MS 365
- Main areas: Models, Knowledge, and Agents
- Hugging Face integration
- Model Router: Help selecting best Model for your purpose
- Azure API Management integration
- GitHub Models UI for testing Model usage and behavior
- Distillation: Break-down a larger Model to a smaller one to save on costs and adjust performance for its intended environment and purpose
- Video: Manus AI builds with Azure Foundry
- Agent services, frameworks (and more)

Demo: Amando Foster, Elijah Strait, Manager and TPM, Foundry

- Using Azure AI Foundry
- Define an Agent in the Agents Playground
- Thread Data: Shows tokens used, and other background factors related to Agent creation
- Foundry Agent Service SDK
- Multiple Agents are available via "A2A" feature

Demo: Patrick LeBlanc, Semantic Operations in PostgreSQL

- VSCode support
- Azure AI Generate function increases agent integration to custom solutions

Video: NASDAQ builds using Azure Foundry AI Agents

Back to Jay:

- Trust and Security: Baked-in to Foundry
- Entra, Pervue, and Defender are built-in to Foundry

Demo: Mehrnoosh Sameki, Prin Prod Mgt, Foundry

- Trustworthy AI Lifecycle
- Measure, Protect, and Monitor
- Test AI Agents against known attacks and get a report on its vulnerabilities
- Set Protection measures within Azure AI Foundry
- Severity Levels are provided to quickly evaluate incident detections
- Defender can identify Agents that could be compromised
- Entra enables removing possibly compromised Agents in real time

Video: Accenture uses Foundry to secure their AI solutions and work toward trustworthy AI solutions.

Back to Jay:

- Cloud vs Edge? Foundry extends capabilities from Cloud **to Edge**
- Microsoft Research: What is possible to build and incorporate into the Azure Foundry platform

Demo: Seth

- Foundry process integrated to an Edge solution (in PowerShell?) ?
- Prediction models help reduce time-to-completion analyzing data (data science work)
- Graph RAG: Ability to import a codebase, generate a Graph (using relational DB techniques, generating Entities etc) to analyse code, find bugs, analyze errors, and add features

Back to Jay:

- Tools and platforms matter
- Provide a deterministic view of what is possible
- Enable use of many Agents (quote: "limitless")
- Constraints on developer count and hours of effort

Demo: Djinder, _____________

- Windows AI Foundry
- GPU, NPU, and CPU
- Local Models available from a directory of AI Models in the Model Catalog
- Locally-executed Models can now run on a Windows PC, with greater capability than just last year
- Phi-4 Reasoning
- Foundry Local: Access, Run, Itegrate high-quality models on Windows platform
- Models are categorized by the target platform capabilities (size, model type, platform, CPU)
- REST Endpoint points to a localhost service to serve, instead of a cloud-based (Azure, etc) :tada:
- Taylor Model behavior via LoRA for Phi Silica and/or Semantic Indexing, Search, and with Knowledge RAG APIs
- LoRA: An adapter that runs alongside the VS Code AI Toolkit
- Use your own training data!
- Create a new project with the Toolkit, select a model, and the training and test data
  - Generating a Project this way gets the project up and running rapidly
  - Fine Tuning tool allows provisioning a Job to run in Azure to train the customized Model
- Demo: Filmora, to demo Semantic Search and the Knowledge Retreival API (a RAG API) to edit a video clip
- Custom Models: Introduce complexity vs. pre-defined models
  - AMD, Intel, NVidia, and Qualcomm all added capabilities for Windows ML

Video: Windows ML use to develop high performance applications

Guest: Charles Lemanna Corp VP of Business and Industry, Copilot

- IDC estimates 1.3 Bi Agents will be built by 2028
- Copilot is one place to put all Agents to work with
- People use app UIs, and Agents will use AI interfaces, in parallel
- Microsoft 365 Copilot "5-in-1 Experience"
- Research, Analyst, Visual Creator, Create Agent, etc
- Agents, Apps, and Collaboration are changing and evolving, all requiring new tools, new thinking, and new ways to get things done (sic)
  - Copilot Studio is the means to make these changes

Demo: Ryan Cunningham, Corp VP, Power Platform Intelligent Applications, MSFT

- CSX Ops is very complex, and Copilot Agents can help
- Plain Language descriptions of knowledge, instructions, and policies
- Connectors used to connect APIs with an Agent
- MCP: Custom or existing, can help pull-in skills and capabilities across agents and applications
- Custom Prompt: Provide instructions, select a Model (even custom Foundry-trained Models), and get a Model Response to see the output
- Not all orgs have an MCP or an API to use for integration, so they will use a specific computer
  - Same tool and processes are used to create and initialize a session to get an Agent up and running
  - This allows an Agent to use a computer just like a person
- Copilot Studio supports "Multi-Agent Orchestration"
  - Can be from various SDKs
  - Custom Model Agents can work collectively to resolve an issue or address a question using their own expertise

Back to Charles Lemanna

- Background and Foreground Agent application experiences
- PowerApps provides a "full stack experience" that allows adding Agents

Demo: Back to Ryan

- Humans are still necessary
- Ability to **unblock** an Agent may require human interaction
- Reporting features like Active Incidents (in Power Apps) help determine where Agents get stuck and enable the ability to unblock them
- Agents can be used to help determine better process flows and relational data models
- Partner with Agents with feedback like "Looks good" and "Edit"

Back to Charles Lemanna

- Collaboration inside Apps and among actual team members
- MSFT "Teams is used by 320 mi people every day"
- Teams AI Library: Build and host Agents to show-up inside Teams

Demo: Farah Shariff, Principal Group Product Manager

- Agents and Bots available within Teams Chat
- MSFT pre-built agent: Facilitator Agent
- Teams AI Library: An SDK supporting conversations, authentication, AI Model integration, etc

Shilpa Ranganathan, Principal Product Group Manager, MSFG

- Securing Agents: Pervue, Entra, etc
- SharePoint Agent integration

Back to Charles Lemanna

- Secure by default using Entra and Pervue
- Entra and Pervue now protect workflows in AI tools

Guest: Scott Guthrie, Exec VP Cloud and AI, MSFT

- There are now over 70 Azure Regions
- DC Capacity is being added incrementally, focusing on AI
- AI Optimized Regions: Mega-scale datacenters!
  - Run "advanced super computers"
- Responsibility: MSFT is purchaing renewable energy
  - Goal is to continue purchaing renewable to match total DC needs
- Cross-laminated timber: Fire-resistant, lower carbon-content
- Lower-carbon content concrete (than "traditional")
- nVidia GB200 AI systems now actively deployed in Azure Dcs
  - GB200's can be interconnected within the DC to optimize GPU-based worklaods
  - "AWS has yet to deploy the GB200 offering"
- Air-cooling is no longer an option: Liquid-cooling is becoming the norm
  - MSFT uses closed-loop liquid cooling systems
  - "Zero water waste": Go-forward method for all new DC designs
- AI WAN: 400 Tb/s bandwidth, interconnects Azure DCs
- Compute VMs leverage Azure Boost to offload virtualization processes to custom silicon
  - Improves local and remote storage IOPs
  - Improves max concurrent connections per VM
- Azure Cobalt 100 VMs
- Street price of using AI is dropping rapidly
  - Building these new generation DCs will help
- Chat GPT: Over 500 mi active users
  - Completely built on Azure
- Data Tier for AI
  - Petabytes of storage required
  - Chat GPT uses aka.ms/CosmosDB with auto replication
  - Azure CosmosDB has built-in scaling capability

## Backstage at Build

Host: Seth

Guests: Stephen Taub, David Fowler

- aka.ms/dotnetmeai
- aka.ms/dotnetmcp
- aka.ms/dotnetaspire

C# is modern, high performance, with batteries-included libraries!

Guests: Scott Hanselman and Mark Russinovich

- CSnakes: Allow running Python code in-process with DotNET
  - Effectively an "Extern C" but for Python
- Hanselman: "Robots are supposed to do things that are Dull, Dirty, or Dangerous"
  - The implication is AI should fit this model, too
- Russinovich: "AI can accellerate what I do, but really cannot completely replace me (sic)"
  - A developer is still necessary to review code output and ensure it is relevant, correct, and is not using deprecated frameworks or APIs
- Induced hallucinations: Propagated ungrounded information.
  - "Gaslighting the LLM" -Scott H
  - "There is **no fundamental means** to prevent LLMs from hallucinating" -Mark R
  - Validation must be used during or "around" the LLM operation to help guardrail (but there are still risks that must be mitigated)
- LLMs must be given permission, and tool(s) to do things with actual code and systems
  - Care must be taken to guard what the LLM actually does with those physical and technical interfaces
- build.microsoft.com

Guests: Divya Venkataramu and Detindar

aka.ms/WindowsAzureFoundry

Host: Seth

Guests:  Anders Hejlsberg and Mads Torgersen

C# and TypeScript

- TypeScript is being ported to Native Code
  - Using Go to get this done due to various managed code and cyclic Types constraints of Rust, C#, etc
- Faster CPUs are no longer the norm, now it's the number of CPUs
  - Languages that cannot parallel multiple threads will not be able to leverage the available compute
- "Syntactic Niceties" in C# lately
  - Collection expressions unifies syntax to initialize effeciently, depending on the actual type, using compiler generation
  - C# leverages the tricks of the SDK and the RunTime to make performance and syntax improvements
- Toolkits and Framework updates
  - Extension Methods (20th anniversary now), now adding Extension Properties and potentially Extending other Members
- Aspire is:
  - Written in C#
  - Supports several languages in addition to C#
- Is AI changing the way we think of programming languages?
  - AI must have languages to target in order to operate
  - Goal is to move further into the deterministic
  - Anders: "Don't ask AI to solve the problem, ask AI to write a program that solves the problem."
  - Also, the training set is critical to getting AI to write a program that solves a problem because older languages are more common and better documented (due to time in the field), therefore more likely AI could utilize it
- Mads: C# team is focusing on removing areas in the language where it is "easy to stub your toe" (sic)

aka.ms/build/languages

## Inside Azure Innovations

Speaker: Mark Russinovich

- Azure Boost:
  - Storage/disk performance (managed, SSD)
  - Networking: dual routers on each rack plus other L2 management and L1 improvements, plus RDMA and offloading
  - RDMA available in general, not just HPC, enabling GPU-to-GPU read/write without software (virtualization offloading) stacks between them
- Updates and reboots
  - Microcode updates: Nearly instantaneous
  - Hot patch: LT 20 ms
  - Driver hot swap: LT 1 sec
  - Hypervisor hot restart: LT 1 sec
  - Live Migration: 2 sec
  - VM-PHU*: LT 20 sec to LT 3 sec
- About VM-PHU
  - "V M Foo"
  - Only freeze a VM **if it is necessary**
  - Allows for **completely restarting the virtualization stack** without VM awareness of the operation!
- AI is pushing very high levels of data storage requirements
  - Throughput improvements enable Tbps bandwidth (compared to 100's of Gbps previously)
- AzureLinux and Linux innovations
  - Security: Use of immutable Linux OS on top of Secure Boot (SE Linux for example)
  - Container Host Policy: LinuxGuard that includes Integrity Policy to enforce what binaries can be run (uses a Container Image Registry in the back that is used for signature verification and policy implementation)
- Sandboxing for multitenancy
  - Protects Linux and Windows containers from each other
  - VMs, Containers, and WebAssemblies
- HyperLight VMs/sandboxes
  - An isolated Micro-VM: "HyperLight"
  - Host Process, Micro VM, and container instance
- New Azure Development Policy: Anyting new must be written in Rust
- Azure Incubations
  - Partner, explore, and delivery industry-changing OSS products
  - CNCF (Cloudu Native Computing Foundation) and Open Governance are focii
- TEE: Trusted Execution Environments
  - Hardware based, 10-year technology
  - Based on Confidential Computing initiative (2014)
  - Now: Confidential AI via confidential GPUs
- Optical Computing
  - Parallel operations
  - Filters
  - Map operations via optice to
  - Leads to the world's first Analog Optical Computer (AOC)

## GitHub Copilot for Skeptics

Speakers:

- Burke Holland, MSFT
- Damian Brady, GitHub

The following statements are partial truths:

- Some damning statements have at least a little bit of truth to them
- They are followed by bullet points of the realities of AI and agentic copilots

It's autocomplete on steroids!

- Not really a fair analogy
- Actually abstract reasoning and latent representation of context
- Ghost Text: An auto-complete on-screen hint
  - Palette: Change Completions Model
- Copilot **will** start guessing
- Blue Arrow Cursor: Next-edit Suggestions
  - Shows a diff of what changes based on its building context, that allows rapid updating

It takes me longer to explain what I want than to just do it myself!

- Modes: Ask, Edit, and Agent
  - Ask: Sandboxed from code
  - Edit: Will edit code, scoped to current selected file
  - Agent: Given vague requirements, it will gather information and make suggestions
- Agent:
  - Will build the code to verify it's own work
  - Available in Visual Studio and VS Code

It's not safe, it writes buggy code, and I'll have to check everything!

- Use of "Diff" views during agent code writing helps to back-out changes that aren't right or not relevant
- Clear the Chat: CTRL + L
  - Often => Keep, Clear, Commit
  - Maintaining a long message history probably isn't helping your code in chat
- Custom Instructions:
  - Define instructions for the Agent to write code in a certain way
  - Define application structure
  - Provide templates for common steps such as component construction (boilerplating)
  - Define best practices (so Copilot doesn't keep selecting different best practices for you)
- Use Copilot to generate Custom Instructions!
  - Iterate through the instructions to ensure they are correct
  - Multiple files are allow, including configuration settings to get custom instructions ready
- Copilot Autofix with CodeQL
  - ALlows simplified, faster correction of Dependabot Alerts
  - Follows Git branching strategy, creating a fix PR for review and/or merge
- Copilot writes and reviews its own code?
  - Yes, don't you do the same?

It's only useful if you don't know what you're doing!

- If you don't know what you're doing, you won't get out of "bad advice" loops with Copilot
- You **need to know what you're doing** in order to get the most benefit
- GitHub Agent Mode can provide information about a scenario, without writing any code
  - Can use tools and frameworks like PlayWright to determine issues with websites and apps
  - Can also create a new GitHub Issue and post it to the repo
- Corrollary: It is incredibly useful **if you do know what you're doing**

It's just a fad, it will pass!

- GitHub Copilot is now over 3 years old
- From ghost-text to assigning Issues to Copilot!
- Human-in-the-loop is still part of the dev loop
- Read through agent session logs to understand what Copilot GH Agent has actually done
- Utilize Copilot Agent to peform work asynchronous to the other developer tasks!
  - "Scale out" your work
  - Segment work for yourself vs. what you assign to Copilot

Who is this technology for?

- Developers: To scale-out their dev loop cycle productivity
- Cognitive Load adjustments:
  - Intrinsic: Doing the actual work
  - Extrinsic: Finding the necessary info
  - Germane: Processing and storing in a cognitive sense
- Using Copilot reduces cognitive load for anyone
- Coding Agent: Implementation summary enables humans to review and/or make adjustments
- In essence: Reduce the total work necessary to complete a task

Change how you think about what you are doing.

## Shift Left: Secure Your Code and AI from the Start

Presenters:

- Neil Coles, AI Safety Empowerment Lead, MSFT
- Marcelo Oliveira, VP Product Mgmt, GitHub
- Mark Russinovich, CTO, CISO, Tech Fellow, Azure, MSFT

Notes:

- Share responsibility to make security a team sport
- AI is changing every role, process, and application
- An expanding threat surface is spanning applications
  - AI further adds to the attack surface
- Secure apps with AI: Code, Secrets, Dependencies, and Infrastructure
- Build secure AI Apps: Models, Data
- Key Issues in code security
  - Alerts with weak signals, lots of noise
  - Security issues are expensive to resolve
- Prioritize solutions based on runtime exposure
- Automate remediation with Agentic AI

Demo: Security Ops Manager of an Enterprise Reduces and Mitigates Breaches

- Azure has codified vulnerabilities that are more likely to lead to a breach
- Apply Risk Factor filters in Azure Defender for Cloud
- GitHub Security Campaigns:
  - Define scope of items that dev needs to address using filters
  - Defender for Cloud integrates into GH Security Campaigns
  - Publishing a campaign with a due date generates Issues and reports on which repositories the Issues are related to
- GitHub Security Tab can review Code Scanning Alerts with suggestions to fix
  - Autofix Validation: Coming soon. Assesses whether fixes comply with code practices and reduce attack surface as well as addressing the problem
- In Preview now: Runtime Context & Agentic Autofix

The LLM At The Heart of an AI Application:

- LLMs are auto-regressing transformers:
  - Next-token prediction machines
  - Non-Deterministic, and as infallible as the humans that created them
  - Can "confabulate" information through searches, inputs, and RAG operations
  - No separation between control channel and data channel
- If risks of a security vulnerability are **too high**
  - Does it make sense to rely on an LLM to fix it?
- Jailbreaking LLM models:
  - Cause a Model to violate its safety and content guidelines
  - There are 100's of ways to do this
  - Skeleton Key, Crescendo, Context Compliance Attack (CCA)
  - Crescendo and CCA are effective in all "frontier" LLMs today
- XPIA: Cross Prompt Injection Attack

In AI, there are still security concerns:

- Secrets, Data, and Access
- AI's are non-deterministic and therefore **will fail**
  - Consider this from the start
  - Otherwise risk of failure are increased
- More layers of mitigation reduce the likelihood that an attack would be successful
- SDL model flattened is: Map -> Measure -> Mitigate
  - Moving right means increasing costs
  - Moving left increases flexibility to mitigate risk(s)
  - Be proactive for effeciency, rather than reactive
- As soon as a product is in design:
  - Find threats through security reviews and threat modeling
  - Modeling: Think about what happens if any one component fails, and how will that help an attacker
  - Mitigate possible issues
  - What are untrusted input sources? Email, form inputs, prompt inputs, etc
- MSFT Purvue will enforce security policies within LLM communications
  - Apps that are **not** Purvue-enabled will not stop working (but security policies won't be applied)
- Defender for Cloud will help strengthen AI security posture from code-to-runtime
  - "AI Security Posture Management"
- aka.ms/MicrosoftLearn/ThreatModeling

## How MSFT Devs Use AI in Real-World Coding

Prsenters:

- Steven Toub
- David Fowler

It's not important to have AI solve the problem for you

- Instead, use AI to help converge on the correct solution
- Iterating over an issue with Copilot can help:
  - **Ideation**
  - Gain a better understanding the problem
  - Additional ideas on approaches to solve a problem (lifting blind-spots)

Simple code-and-throw-away tools:

- Allow Copilot to build the solution as much as you want
- It helps to have some knowledge/expertice in the area
- Short-lived project or tool that is needed for:
  - Proof of concept projects
  - Implementing a very specific, or one-off task
  - Exploring new or not well understood concepts in preparation for further development

Handling difficult issues in a repo:

- Very complex issues in a codebase can be pushed back over and over again (technical debt builds)
- Addressing the problem might require brain-trust from multiple players
- Utilizing Github Copilot to gain insight into the problem, and identify areas where expertice in needed will help get the ball rolling toward a solution
  - Security SMEs
  - Multi-threaded programming SMEs
  - Framework SMEs
  - Architects
  - etc

Documentation

- Sometimes documenting code can have benefits for the writer, such as self-reviewing code while writing doc strings
- However, documenting a large number of public members can take a very long time and be tedious work
- Use Copilot to write the documentation for you:
  - One or a few docstrings: Start the comment in-line and let Auto-complete do the rest
  - Many docstrings: Ask Copilot to document the public methods on an entire codepage
  - Analyzing existing (but very poor, not well understood) documentation to improve it

Creation

- Feed well-specified features into AI to get a sense for approaches to solve
- Iterate with the AI to converge on working, testable code
- Use performance analysis tools to A:B test against the spec
- **Review the code** and **make adjustments** as necessary to meet:
  - Code standards
  - Add comments
  - Refine areas where specifications aren't met e.g. max value, min length, etc

Testing

- Introduce the SUT to the AI
- Request unittest code from the AI
- Review the test code
- Use Github Copilot to review test failures and get candidate code fixes (to the tests or the SUT)
- Write a couple tests, then ask the AI to write the (dozens?) of others that are needed

Taub on Ghost Text: "Write 2 of 40 methods, then tab your way to glory"

Bugfixing:

- Assign GH Issues to Copilot and have it generate a possible solution
- Human engineers can review Copilot proposed fix, and complete the PR workflow

## Under The Hood And Into The Magic Of GitHub Copilot

Presenters:

- Christina Entcheva, Sr. Dir of SW Engineering, GitHub
- Christopher Harrison, Sr. Dev Advocate, GitHub

How Requests are Processed:

- LLMs can: Generate text, translate languages, recall info, break-down problems into steps, and recognize and predict patterns
- LLMs are limited by: Specialized domain expertise, perfrect acuracy, untrained knowledge. real-time data access
- Copilot is:
  - Trained on lots of public code
  - Patterns, practices, and patterns
  - General knowledge
  - Code quality and safety training
  - Trained to avoid legal and ethical risks
- Copilot cannot:
  - Understand the full context of your code repo
  - Generate new solutions (limited to what it's seen before)
  - Access live APIs to complete it's charged tasks
- Flow: Input, context analysis, user-intent, response generation, rank and filter suggestions, response generation return, user feedback received, refinement returned to context analysis
- Tokens are broken-down segments of words
- Sliding/Rolling Context Window processes relationships between tokens
- Context Chunking: Headings and content are chunked to arrange for generated responses
- Prompting:
  - gh.io/custom-instructions
- Planning: Copilot generates requests into steps necessary to complete a request
- Include the right context:
  - More context is **not always better**
  - Arrange your input context accordingly

Working in the IDE:

- Code Completion:
  - "Ghost text"
  - Good when you know what you're doing but need just a little help
- Next Edit Suggestion:
  - Newer than Code Completion
  - Support across entire file-based on changes being made
  - Good for refactoring and performing updates
- Context while coding:
  - No UI for selecting content
  - Balance context and speed
  - Match common coding patterns
- Set context for code completion and NES
  - Open files are part of the context (naturally)
  - Open an example of a library as an example for Copilot to use
  - Close all open tabs and restart to switch the Context effectively
- Reset context when moving between parts of a project
  - Start over the context to avoid pollution from no-longer-relevant context
- Chatting:
  - Ask: Simple, single file, single task
  - Edit: Dev-led multi-file edits
  - Agent: Copilot-led, multi-file editing and creation
- Context:
  - Add files
  - Use experts
  - Utilize `@workspace`
- Instruction Files
  - Repo wide, every Copilot request, becomes part of the Project: `copilot-instruction.md`
  - Task specific with `{name}.instructions.md`: "Instructions files" defining frameworks in use such as ASP.NET Core, Node.js, or code style instructions
  - Think about how chat queries are used, and apply definitions to these files so Copilot reads them **as part of your prompting**
- Selecting a Model
  - "Play and explore" -Christopher H.
  - Thinking or Reasoning: Best used when going through Ideation cycles

Working on GitHub.com:

- Good for:
  - Understanding and Navigating code
  - Repository context
- Issues and PRs
- Can generate a project based on uploaded wireframes and high-level design instructions

Demo: Generating Code from Images

- Mobile ToDo App
- Ask to generate code based on an attached wireframe, defined framework, app architecture overview, and code language
- Copilot drafts a PR

Agent Mode:

- Asynchronous!
- Follows steps as a developer would
- Like Edit Mode, but adds autonomy
  - Edit Mode: Developer leads the conversation and development
  - Agent Mode: Developer tips-off Copilot's work, which it then does **on it's own** but **with developer control**
- It is still necessary for the developer to control the process from start-to-finish
  - Team responsibilities are still in effect
- Can interact with MCP Servers!
- LLM's on their own cannot find information on the fly
  - MCP Servers enable this capability
- `mcp.json` defines inputs, servers, and credentials in order to perform actions and use tools
  - Use environment variables, secrets, tokens, etc

Demo: Agent-Mode Project Creation

1. Add an instructions file to tell Copilot what you want done and **how** it should be done
1. Supply additional file(s) as necessary to bolster context with examples
1. Continue working in Chat or Chat Edits and Copilot will use prompts and instructions to complete the task

Copilot Coding Agent:

- Uses semantic and lexical search
- Full repo contenxt enabled
- GitHub MCP Access
- More about [code search](github.io/features/code-search)
- Agent includes safeguards:
  - Uses own branch
  - Read-only access to your repo
  - Action Workflow won't run without review
  - Won't review own Code in PRs
- Provide clear, scoped issues
- Provide custom instructions file
- Customize the dev environment for Copilot
- Configure MCP access to solve problems requiring current, internet-accessible data

Question about File Exclusion:

- Tells Copilot to not consider a file **at all**
- When prompting Copilot, tell it to **not** edit the file(s) that shouldn't be changed

## Use VSCode To Build AI Apps and Agents

Speakers:

- Lori Fraleigh, Principal Group PM Manager, Azure SDKs, MSFT
- Rong Lu, Principal PM Manager, MSFT

Brief overview of how AI Agents work, then Demos!

- User -> Prompt -> AI Agent -> Response
- AI Agents process prompts using Models
- Model Tools include: APIs, DB, Web, etc
  - MCP protocol enables these!
- TypeSpec: OSS language/tooling
  - [TypeSpec](https://typespec.io)
  - Similar to Open API definitions
  - TypeSpec Definition files `TSP` define the TypeSpec specification: `main.tsp` etc
  - Server configuration is `mcp.json` in `./.vscode` directory
- MCP Servers can run locally or in the cloud
  - Sent-Events are used to communicate back and forth

Note: Demos were done using TypeScript.

Demo: Build a Local Agent that calls three MCP Servers

1. Build a TypeSpec MCP Server using VSCode, GitHub Copilot (Agent Mode)
1. Add new tool definitions to the MCP Server
1. Add new tools to the code by adding Tool Methods

- [TypeSpec MCP Server generation](aka.ms/mcp/tsp)

Demo: Add AI Agent to MCP

- Use VS Code AI Toolkit Extension
- Multiple Models can be selected
- Use Playground to view token usage, test prompt results, and responsiveness of the model(s)
  - Determine which Model is best suited for your project
- Use Agent (Prompt) Builder:
  - Select local and remote Models
  - Create a prompt template with detailed steps that teach the Model how to work
  - Defining MCP Server descriptions will help the Model do the right thing
  - Define Tools: Allows developing or use existing MCP Server(s) into the Agent
- `{name}agentSchema.json` provides metadata about how Responses should be structured
- Variables can be defined
  - Single variable using `{{variable}}` where data can be typed in manual
  - Use of an Evaluation Data Set file and

Demo: Move local Agent processes to the cloud

- Leverage Azure Container Apps (ACA)
  - Note: Costs/sec, scaling, etc
- AI Foundry Service will be used for configuration and management
- Use `azd up` to initialize Containers in ACA
- Utilize VS Code Azure Foundry Extension
  - Creates an in-IDE Azure Foundry Portal UI for management
- Create a new Agent
  - Is a YAML file
  - Extension includes a designer view as an option to config YAML elements (or view results of YAML configuration entries)
  - Intellisense should help build the YAML file using your project context
  - Sliders to edit Agent Settings like Temperature and Top P
- There are built-in Tools for things like
  - Custom MCP Servers
  - Other connections already configured in your subscription
- Use Agent Playground to test the defined Agent configuration
- Threads (in Azure AI Foundry) displays logs of actions taken by an Agent

Reminder: `mcp.json` defines MCP Server endpoints, both local and remote.

Relevant Links:

- [AI Developer Tools](AIDevTools/Build2025)
- [Install: AI Tools Pack](AIToolsPack)
- [Try: TypeSpec MCP Server](mcp/tsp)
- [Deploy: MCP Server Container App](https://aka.ms/mcp/aca)
- [Develop OpenAI MCP Agents](https://aka.ms/mcp/openai)
- [code and resources](https://aka.ms/BRK117)

## Top GiHub Copilot Features You Missed in Visual Studio 2022

Speakers:

- Simona Liao, Product Mgr, VS GitHub Copilot, MSFT
- Rhea Patel, Product Mgr, VS GitHub Copilot, MSFT
- Filisha Shah, Sr. Product Lead, VS GitHub Copilot, MSFT

The Copilot AI Journey

- Prompt experiences are improving:
  - Ghost-text in IDE
  - Chat in IDE
  - Autonomous and Agentic flows in IDE and on GitHub
- Prompt-first focus
- Editor-centric experience focus

Agent Mode Is Now Live in Visual Studio!

- Gives a little bit of brain and a pair of hands to Visual Studio
- Think of Agent Mode as an AI Teammate instead of an assistance

Tool Calling:

- How Copilot knows how to access tools
- Can view or add to an existing code page
- Enables some self-healing-like behaviors
  - The demoed situation was a weird error state during debug-time that Copilot solved

Iterating Editing:

- Enabled through Tool Calling
- Loops through code making changes until the end goal is met

Image Recognition:

- Copy-paste an image into the Chat Window
- Provide prompt text to describe the task to accomplish
- Copilot will analyze the image and use as part of the generated response

Custom Instructions:

- Define preferences around code styling
- Describe the project to outline its basic design at a high level (front-end, back-end, SPA, etc)
- Assert specific tools be used for specific tasks such as an image processor

MCP Servers:

- Plug in things you are working on to Copilot
- Reads and acts on information using MCP Servers and their tools
- `mcp.json` defines services with IO type, custom commands (and a collection of args), and necessary environment variable references, and the type of command such as "promptString"
- Can be turned-on and off at the GitHub Organization level
- Control MCP Server access, restricting to specific server(s), or using none, etc
  - Detected changes in MCP settings will cause a prompt asking for approval

Coding Agent:

- Now available (in preview?) in Visual Studio
- Runs autonomously and asynchronously
- Ask `@github` to create a PR based on the prompt request
  - Can be associate with Issues in GitHub
  - Creates a draft PR
- Generally different than the GitHub Copilot Agent

How does Copilot support my wanting to maintain control as the developer?

- Copilot Completions: The O.G. code suggestion maker
  - Occasionally gives new results when not wanted
- Next Edit Suggestions (NES)
  - Prediction of next edit
  - Assist anywhere in the file
  - Availbale in v17.14 Preview 3
- Tab Completions still in-effect
  - Up/Down arrows in Tab Completion icon show where more predicted changes are being displayed
  - Pressing Tab again moves the cursor to that next suggestion
  - Pressing Tab yet again implements the change

Adaptive Paste (preview):

- Tools -> Options -> Copilot -> Editor -> Enable Adaptive Paste
- Copy C++ code, past as C# in the editor!

"Good developers not only write good code, they copy-paste **great** code!" -Simona Liao

Quick Actions (lamp or screwdriver):

- Good for code generation and modification
- Navigation to next changes/matches/suggestions

Other Features:

- Implement with Copilot, prompted with `NotImplementedMethod` text
- GitHub writes commit messages
- Set up GitHub PR within VS IDE
- Copilot-generated code-comments, prompted with `///`

## Elevating Development With .NET Aspire

AI, Cloud, and Beyond!

Speakers:

- Damian Edwards, Principal Architect, MSFT
- David Fowler, Distinguished Engineer, MSFT
- Maddy Montaquila, Sr. Prod Manager, .NET Aspire, MSFT

Aspire wants to be the cornerstone to the developer experience:

- Agentic Apps
- Agentic DevOps
- Cloud, Web, Desktop, Mobile, Data, and Services
- Local dev is **fragile**
- Scripts, hacks, and tribal knowledge is commonly used in critical workflows
- Improve dev onboarding, enabling instrumentation, setting resiliency, encourage pluggability

Demo: Aspire in the wild:

- Guest: Devis Lucato, Office of the CTO, dev.ai
  - Aspire power user and fan!
- Focus: Kernel Memory AI Service codebase
  - "A web service as a Docker container with plugins for ChatGPT/Copilot/Semantic Kernel and other LLMs"
  - Many tools and scripts necessary to build and maintain the pipeline for this multi-platform capable project
- From now on: Start new projects with Aspire and go from there
  - Starts all dependent services and tools automatically
  - Writing docker-compose takes longer than updating AppHost (Aspire)

Aspire Benefits:

- Code-first control
- Modular and extensible
- Observability from the start
- Flexible deployments
- Heavily used in MSFT and by MSFT Partners

Aspire releases:

- Aspire 9.3 is out this week
  - Includes Copilot!
- Roughly 6-week release cycle
- Step-away from Aspire Workloads (over 1 year old, no longer maintained)
- Install Aspire templates if not installed already
- Update Aspire Templates: `dotnet new update`
- Update Nuget Packages in the `csproj` or use Package Manager, etc
  - Option: `dotnet outdated -inc Aspire -u`
- Package-based Sdks are not updated by command-line tools nor Nuget Manager
  - Instead, update the "Aspire.AppHost.Sdk" entry with "version=9.3.0"
  - AspireApp Service Defaults csproj will also need to be updated (`dotnet outdated -inc Aspire`)

New Features:

- GitHub Copilot
- Resource Graphs and Tables
- Additional Resource Actions in context drop-downs

Comming Soon:

- Cmd-line experience: `aspire ...`
- `dotnet` command equivalents are run all in one shot
  - For example: Includes Dev Certificate installation on `new` command
- `aspire new` -> Like `dotnet new` but Aspire-focused
- `aspire run` -> Same as VS Code/Visual Studio run button
- `aspire add` -> Curates dependencies for other ecosystems including node, AI model packages, etc
  - Basically shows Aspire-filtered tools
- `builder.Add{nnn}App()` and point to the configuration file
  - Node-based would need `package.json`
  - `.WithHttpEndpoint(targetPort: nnnnn)` to point to a port that Aspire doesn't manage directly
  - Use `Node Extensions` to work-around issues like forgetting to `npm install`
- `aspire` commands: `new`, `run`, `add`, `publish`

Aspire helps with the SDLC:

- Onboard -> Develop -> Test -> Deploy
- Deploy: Uses `azd up` to make deployment magic
- Deployment is very complex: Tools, custom scripts, workflows, architectures, etc
- Story: Deploy to ACA
  - Evolution from single environment to an expressed intent for complex deployments

AppHost:

- Good high-level view of the entire application
- Review configuration, dependencies and needed parameters
- Describes Application **to Aspire**

Getting Your App Into The Cloud:

- The idea is AppHost models a production deployment
  - Based on actuals in the dev environment
  - Can (will) target various environment types/platforms, project-by-project
  - Longer-term goal: Glue the projects together including networking, etc
- Once AppHost is completed, point a toolchain to it
  - Some additional tweaks might still be necessary
- Aspire 9.2.x has package `Aspire Hosting App Containers`
  - `AddAzureContainerAppEnvironemnt("env")` adds items via IComputeResource interface
  - "Treat AppHost as the configuration descriptor" - David F
- `azd infra synth` -> An alpha product produces compute resources targets
  - Produces an `infra` directory
  - Adds Bicep files that represent AppHost configurations
- Split-deployments: Front-end in one service, back-end in another
  - Use `.WithComputeEnvironment(string)` for each project definition
  - Will generate directories for each defined environment
  - Actual app expressions (Bicep files etc) will represent the target environment type

.NET Aspire References:

- [.NET Aspire GitHub repo](github.com/dotnet/aspire)
- [.NET Discord](aka.ms/dotnet-discord)
- [.NET Aspire Home](aka.ms/dotnet/aspire)

## Yet Another Highly Technical Talk

Speakers:

- Scott Hanselman, VP Dev Community, MSFT
- Stephen Toub, Partner Software Engineer, MSFT

Deep Dive Into The Threading Channels Library:

- Channels is actually really small, and not that hard
  - But it seems really complex
  - Locking, Queuing, and Notification
  - Is just a data structure like List or Queue
  - Channels **are the synchronization primitive** in Go
- Channels: [System.Threading.Channels](https://learn.microsoft.com/en-us/dotnet/core/extensions/channels)
  - Part of .NET Core
  - NuGet package for .NET Framework
  - Allows implementing Consumer-Producer solutions
- Unbounded: No artificial bound on the capacity
- Asynchronous, Task-based
- Useful for:
  - Passing data by "throwing data over the fence" from Source to Consumer
- DotNET Index website [source.dot.net](https://source.dot.net)
- Three primary members:
  - `ValueTask WriteAsync(T item)`
  - `void Complete()`
  - `ValueTask<T> ReadAsync()`
- Actual datastore can be a `Queue<T>`
- Synchronization control necessary:
  - `object SyncObj...` can be used for locking
  - Implement it like `lock (SyncObj) { ... }`
  - The code-block code will trigger the lock and release it when it exits
- Use `TaskCompletionSource<T>`
  - Used as a means to start a Task
  - Later on it can be 'poked' to get the Task Result
- Upon completion, tell consumers there are no items left
  - Using an Exception? Probably not the most effecient way to do this
  - Calling throw? Instead, return a ValueTask that contains an exception instead
  - Follow async-await contract obligations
- Generics and Nullable Reference Types:
  - Interesting relationship
  - Consumers might not know T could be null
  - Use an annotation like `[MaybeNullWhen(false)]` identifies **when** the result is actually null, otherwise it is **not nullable**
  - Contrast to T? which says it might **always** be null
- Waiters need to be notified!
  - Waiting readers need to be set the result of `false`, then nullified
  - This is the "putting a result in an envelope without you knowing"
- Use Visual Studio Parallel Stacks window to help debug
- Calling Continuations is the core implementation for "waiting" code finding out if it should pick up and run from where it left off

Note: Do not expect this stream of comments to be useful other than a fond memory of the session as it was, learning new stuff along the way.

## Debug Like A Pro: Improve Effeciency With Visual Studio and Copilot

Speakers:

- Charlie Aslan, Principal Software Engineer Manager, VS Debbugger Team, MSFT
- Harshada Hole, Sr. Product Manager, VS Debugger and Profiler Team, MSFT

Essential Copilot Features for Debugging:

- Locating problematic code in Run Time:
  - Small codebases this can be straightfoward
  - Ask Copilot to describe symbols from the popup window
- Context Elements
  - Start with '#' hash symbol
  - Solution: All projects in the current Solution
  - Ask Copilot to find code that does {something}
  - Declare your intent, and Copilot will figure it out and show you the code
  - `#Debugger`: Use to request info on the current RunTime Thread at a breakpoint
- Ask Copilot "fix bugs" in the Active Document (default)
  - Potential problems will be listed
  - Will provide Fix statements for areas with code smells
- Utilize different Model and ask the same question
  - Occasionally, different issues could be found
- Context is important
  - Go for fine-targeting context, not more context
  - Screenshot the running app UI when the problem is happening, tell the model the intent, and it should come up with possible causes
- Apply suggested changes
  - Copilot suggestions can be applied with a button
  - Also, copy-paste code segments can also be performed
- Steer Copilot with follow-on intent statements
- Breakpoint debugging
  - Breakpoints can be disabled
  - Breakpoint rule can be set on each Breakpoint to conditionaly enable it
  - Setting Breakpoint(s) at specific locations
- While in break mode:
  - Review the data in the current state (Members with values)
  - Use the View Visualizer to get a better formatting of data in lists or objects
  - Copilot Sparkle in Visualizer allows prompting to perform filtering based on existing data view
- On a Exception thrown:
  - Click "Analyze with Copilot" to get analysis, get a view of the data (in this case the REST Response payload), and accept code changes
- Execution Point edits:
  - Drag the pointer back in time to re-run code
  - Even edited code that is backed-up and re-ran will be re-evaluated!

Use Debugging with Copilot to work with a code language you **aren't familiar with**.

Use Parallel Stacks window to get details on all Threads and Stack Calls in a visual graph-and-table format.

## Build The Next Gen Of AI Apps With DotNET

Models, Data, Agents, and More

Speakers:

- Jon Galloway, MSFT
- Brady Gaster, MSFT
- Jeremy Likness, Principal Product Manager, .NET and AI, MSFT

Fast-paced Technology Movement:

- ChatGPT released in 2022
- Specialized libraries for using AI used to be the norm, now are all available through .NET

Jeremy: AI on .NET

- Generative AI apps are being built on .NET
- Growing .NET AI ecosystem
- Microsoft.Extensions.AI, VectorData, MCP Server, AI Templates, Semantic Kernel, and Model Evaluations
- Ollama Sharp: DotNET Library with Microsoft AI Extensions, for local development (requires GPU and/or larger compute power)

Jon Galloway:

- New startup experience: `dotnet new install Microsoft.Extensions.AI`
- After dotnet new, start a new Project and select an AI Template
- AI Service Providers can be selected within the template
- GitHub Models is **free** but is token-capped
- OpenAI and Azure AI are other options
- Vector Store can be local (json files on disk, for prototyping), Azure AI Search, or Qdrant
- Relies on Aspire Orchestration
- Template README has instructions on how to get started
- Use `Manage User Secrets` at the project level for setting tokens, etc
- DataIngestors can process input files such as PDFs that are used by the Model
- Adding an AI in DI using AppBuilder allows swapping-in a different AI Model without having to change any business logic, UI, etc
- Inject (`@inject`) `IChatClient` to tie together the AI Model injection, and the UI and business data

Jeremy: Agents

- Agents are LLMs that are enhanced by various service and tools
  - Tools like MCP
  - Memory like state management
  - Data from RAG
  - Orechstration for routing and scaling
  - Workflows for agent automation
- Think of an AI Agent as an interface
  - Generate, Retreive, then take Action
- Use Kernel.CreateBuilder to make AI Extensions "agent ready"
  - Interfaces agents
- Many Agentic Apps at many levels via .NET

Brady: MCP SDK For DotNET

- [Model Context Protocol GitHub Repo](https://github.com/modelcontextprotocol)
  - THe csharp-sdk is found here
- McpServerToolType: Identifies a tool that an LLM can use to access external resources
- McpServerTool: Identifies methods that are available to the enclosing McpServerToolType
- Description() attribute: Plain-text explanation that the LLM can process to help it manage execution of registered tools
- Chat will prompt the user to allow accessing custom code and external resources when calling custom McpServerTool resources

Jeremy: How do we get from prompt to results?

- Uses Semantic Kernel Process Endpoints
- Route requests to correct Agent based on User Intent
- Get the user intent, pass the intent to the Agent(s), then process the results
- Use Aspire to define non C# apps such as Python, Node, etc
- Eval Framework:
  - Ensure content is safe
  - Integrate with test harnesses to validate prompt, processing, and response
  - Provides an Evaluation Report of retreival accuracy
- Link to [project code](https://aka.ms/dotnet/agents/build25)
- DotNET 10 release date: 10-Nov-2025
- Link to [DotNET AI App Template Info](https://aka.ms/create-dotnet-ai-apps)

## AI Infused Mobile and Desktop App Development with .NET MAUI

Speakers:

- Beth Massi, Principal Product Manager, .NET MAUI, MSFT
- David Ortinau, Principal Product Manager, .NET MAUI, MSFT
- Gerald Versluis, Senior Software Engineer, .NET MAUI, MSFT
- Uma Maheswari Chandrabose, Sr Prod Mgr, Essential Studio, Syncfusion

MAUI Notes:

- MAUI use is still growing, YoY
- Increased OSS participation
- Look at using ONNX framework to integrate AI
- Plugin.Maui.Audio: Cross-platform plugin
- MediaPicker: Updated and fixed
- Syncfusion Toolkit: OSS Controls for .NET MAUI

How is MAUI Team Thinking About AI?

- Infusing AI into MAUI Apps
- Work smarter, not harder
- Agentic Apps: App building for cloud, web, desktop, mobile, games, and IoT
- Agentic DevOps: CI-CD, GitHub Actions, etc

Disruption:

- AI adds a "3rd user interface" paradigm *[Jakob Nielsel]*
- Focusing on what you want the app to do, rather than **how** to do it
- AI changes applications:
  - How the work
  - How we develop them
- Adds Personalization, context-awareness, multimodal interaction

Demo an AI-infused App:

- Create a new MAUI project with the Samples to get starter components and functionality
- Granting access to phone features allows it to know a **lot** about you
  - Where you are
  - Ambient light conditions
  - Network connectivity
  - Connected apps
  - etc
- Agentic apps can filter-out garbage words and focus on key words that will produce valuable results

Video:

- Using the phone camera
- Look at a recipe and make a shopping list with just a prompt
- MAUI provides a platform for delivering a simplified, capable UI
- Enable optin-in to get more features

Design:

- Take a peek at "Design principles for Generative AI Application" Weisz, He, Muller, Hoefer, Miles, et al, Werner Geyer International Converence on Human Factors in Computing Systems 2024
- Design Responsibly
  - Solve **real** user problems
  - Minimze user harm
  - **Test**
- Design for Mental Models
  - Teach AI about the user to align with their mental models
  - Ensure user is introduced to "generative variability"
- Design for Appropriate Tust and Reliance
  - Be clear on how well AI performs for given tasks
  - Use friction to prevent overreliance
  - Encourage critical thinking
- Design for Generative Variability
- Design for Co-Creation
  - Help user craft effective outcome specs
  - Provide generic input params
- Design for Imperfection
  - Make uncertainty visible
  - Evaluate outputs for quality
  - Provide feedback mechanisms
- There are many more points, see the reference at the top
- Microsoft has AI Principles too:
  - Fairness, Reliability, Safety, Privacy, Security, Inclusiveness, Transparency, Accountability
- Mitigation Layers
  - HAX Toolkit, System Message Framework, AI Content Safety, AI Foundry Model Catelog

Syncfusion:

- Guest Speaker: Uma
- Comprehensive suite of over 1900 UI Controls across various frameworks
- Targets mobile, web, and desktop

DotNET MAUI Hybrid Apps:

- Blend Native and WebUI technologies
  - HTML, JS, CSS wrapped in a Native App Container
- Mobile and/or Desktop apps!
- Access to native features
- Reuse WebUI and redistribute within a Native App e.g. via an App Store
- WebUI + NativeUI:
  - Look and feel
  - UX is seamless
  - Code Reuse
  - Skillsets: Web + XAML
- Types of Apps Controls:
  - Blazor Web View: Solution templates, hot reload, auth, validation, etc
  - Hybrid Web View: Include other web frameworks like Vue, React, and any JavaScript interop
- New Hooks for intercepting web requests coming in .NET 10
- Syncfusion Controls are now available for Blazor
  - These are responsive (by default?)
- Inject the needed dependencies to enable hybrid
- Just use `<BlazorWebView.RootComponents>` component in the Native portion

Agentic DevOps:

- DevOps is evolving:
  - DevOps -> DevSecOps -> Agentic DevOps
  - All enable continuous delivery, value, automation, acceleration, and optimization
- GitHub Copilot is built for developer experience
  - Automate the mundane
  - Pay more attention to what matters
- Copilot Vision can import images to help develop the UI for you
  - Supports XAML!
  - "Implement the XAML for the attached image of ..." :tada:
  - "Implement the UI according to this Figma design at url ..." :tada:
- Coding Agent
  - Issues, PRs, code edits, commit and comments, and code review comments
- DotNET Aspire:
  - VS Future Feature: Enlist Aspire to my app in a right-click menu
  - Handles multi-project startup configuration including MAUI, including Hybrid
  - Add MAUI project then `.WithReference('webapi')` to tie-it to the Blazor portion
  - Will launch the Android Emulator!
  - Copilot integration allows help with resolving issues based on Structured Logs, etc

MAUI Resources:

- Contact David O. to get closer to the .NET MAUI team
- [Resources for this session](https://aka.ms/RAI)
- [Syncfusion.com](https://syncfusion.com)

## Scott and Mark Learn To... Live

Speakers:

- Scott Hanselman, VP Dev Community, MSFT
- Mark Russinovich, CTO, CISO, Tech Fellow, Azure and Cloud, MSFT

Hello Robot:

- Demo integrating Agentic AI with robotics
- Guest: Muhammed from HelloRobot
- OS Robots platform
- Target users: Students and undergrads
- Robot is:
  - HelloRobot Stretch :tm:
  - Intel NUC i5
  - Segway-like robot base
  - Telescopic arm
  - Cameras to view grip, movement, etc
- Scott added an ARM-based laptop to control the ARM

Design:

- Semantic Kernel used for orchestration
- Realtime Agent to provide a human voice using OpenAI 4o mini
  - Go for local, smallest models, that are able to talk to the cloud if necessary
  - WSL with Robot-Agent to get tasks to fire
  - C# and Python code
- Image captioning and Semantic Sensor
- Utilize NPU, CPU, and GPUs appropriately
- TCP Sockets used to send functions and assign tasks
- Planning: Create a Workflow
- Execution: Acts on the Workflow
- Human Control: Visualize the plan and enable approval
  - Human-in-loop is a critical component in utilizing AI

Usage:

- Aruco code symbols allow Eye-on-hand to evaluate size, tilt, distance (etc) of an object in view

Tools:

- AI Dev Gallery

New Info:

- Project Roma
- Defense XPIA by controlling the flow of information
- Adds a Baseline Orchestrator to track information as it moves through an Agentic System
  - Prevents LLM from seeing data that doesn't match a policy
- XPIA is **still and unsolved problem**

About AI: "They don't know what facts are" -Mark Russinivich

## Definitions

### Model Context Protocol (MCP)

RAG: Retreival Augmented Generation.

Open-source framework defines how AI models share data with other tools. Consider this like HTTP, where common capabilities are defined for web-based client-server communications. MCP enables AI assistances to exchange info with varying software environments. Originally developed by Anthropic in Nov 2024. Adoption is accelerating.

The CSharp SDK supports MCP, exposing interfaces to easily implement MCP and interact with other MCP-compliant clients and servers.

Check out James Montemagno's YouTube video [Beginner's Guide to Building a MCP Server with C# and .NET](https://www.youtube.com/watch?v=MKD-sCZWpZQ)

### Setup MCP Server Notes

- There is a CSharp SDK for MCP Server creation
- Utilize ApplicationBuilder to build-up and configure the MCP Server in DI
- Attribute "[McpServerTool]" marks methods as MCP-related tool definitions
  - Finds tools in the MCP Toolkit
  - Exposes custom Tools (dev-defined Methods) that MCP will use
- `mcp.json`: Configure the server with commands with arguments, similar to Node `Package.json` or VSCode `launch.json` and `tasks.json` files
- Use Copilot AgentMode to get MCP interaction

Build new tools:

- Generate class file(s) to define the tool state and functionality
- Inject the tools into the MCP DI
- Use attribute `[McpServerToolType]` to define the Tools Class that will contain the tool methods
- Add attribute `[McpServerTool, Description(string)]` to expose the Method as a Tool capability to the MCP Server

CSProj Integration With Docker:

- Enable SDK Container Support
- Point to a Container Repo
- Define a base image for the container
- Assign a RunTime ID to define what architectures to bundle-up in the container
- These enable calling `dotnet publish /t:{container}` to push to a Docker Container
  - Also enables dotnet to publish Containers to Docker (James demonstrated publishing to his personal Docker Repo)
- With the Docker Publish, the `mcp.json` can be set to point to a Docker Container rather than a local dev machine instance!

## Thinking Forward

A list of things that interested me and could become future tasks to complete:

- [ ] Review [D3js Chart Building Framework](https://d3js.org/getting-started)

## References

- [Beginner's Guide to Building a MCP Server with C# and .NET](https://www.youtube.com/watch?v=MKD-sCZWpZQ)
- YouTube video [Taub and Fowler: How MSFT Devs Use AI](https://www.youtube.com/watch?v=gieL0bxyTUU)
- [Global AI Community](https://globalai.community/) AgentCon 2025 was on 1-Apr-2025
- [Developing next-gen cancer care management with multi-agent orchestration](https://www.microsoft.com/en-us/industry/blog/healthcare/2025/05/19/developing-next-generation-cancer-care-management-with-multi-agent-orchestration/)

## Footer

Return to [ConteEd Index](./conted-index.html)

Return to [Root README](../README.html)
