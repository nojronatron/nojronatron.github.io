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

## Definitions

### Model Context Protocol (MCP)

RAG: Retreival Augmented Generation.

Open-source framework defines how AI models share data with other tools. Consider this like HTTP, where common capabilities are defined for web-based client-server communications. MCP enables AI assistances to exchange info with varying software environments. Originally developed by Anthropic in Nov 2024. Adoption is accelerating.

The CSharp SDK supports MCP, exposing interfaces to easily implement MCP and interact with other MCP-compliant clients and servers.

## Thinking Forward

A list of things that interested me and could become future tasks to complete:

- [ ] Review [D3js Chart Building Framework](https://d3js.org/getting-started)

## References

- [Global AI Community](https://globalai.community/) AgentCon 2025 was on 1-Apr-2025
- [Developing next-gen cancer care management with multi-agent orchestration](https://www.microsoft.com/en-us/industry/blog/healthcare/2025/05/19/developing-next-generation-cancer-care-management-with-multi-agent-orchestration/)

## Footer

Return to [ConteEd Index](./conted-index.html)

Return to [Root README](../README.html)
