# Microsoft Build 2023 Notes

Twitter: @msdev, #MSBuild

Official [Build Playlist (Spotify)](aka.ms/buildplaylist)

## Keynote

Speakers and Demonstrators:

- Satya Nadella - CEO
- Kevin Scott
- Yusef Mehdi
- Scott Guthrie, MSFT EVP Cloud and AI
- Thomas Dohmke, CEO GitHub
- Seth Juarez, Principal Program Manager, MSFT
- Sarah Bird, Partner GPM, Responsible AI Lead, MSFT

Book: As We May Think - Vanner Bush

A "Mosaic Moment"

How Developers build software is fundametally changing.

- Codespaces
- Microsoft Dev Box
- GitHub CodePilot & CodePilot X
- GitHub Actions and Azure Develpment Environments

Top Five Announcements:

- Bringing Bing to ChatGPT
- Windows Copilot: ChatGPT will help configure Windows for productivity and focus, as well as integrate with other Microsoft tools e.g. Microsoft 365, Office, etc.
- Copilot Stack: Apps, Orchestration, and Models and AI Infrastructure
- Azure AI Studio with Azure AI Safety: Testing, Governance, Deployment.
- Microsoft Fabric: Data analytics for the era of AI.

Build with safety first.

Why do we build technology?

- Help drive economic growth.
- Improve health and standard of living.
- Develop platforms to allow building value on top of it by everyone, simplifying the processes of building complex solutions.

The era of AI Copilot News from Kevin Scott - CTO and EVP of AI, MSFT, and 'Behind the Tech' Podcast.

- MSFT + OpenAI
- Azure: The cloud for AI
- Windows and AI Development (Windows Copilot and more)
- Copilot: Using Modern AI to asisst with complex cognitive tasks

Copilots:

- Must be an open ecosystem.
- Encourage open-sourced solutions.
- ChatGPT, MSFT Security, MS 364, Designer, and many more Copilot tools.
- Become a platform: Others gain more benefit than the platform builder (see Bill Gates quote about what a Platform is).
- Plugins enable your application to do what you need it to do using Copilot.
- _Act safely_ on the user's behalf. Example: Allow the user to review information before posting it to social media.
- Developing Copilot UX, Architecture, and Safety and Security.

When Building a Copilot:

- Must build a _great product_.
- The model _is not_ your product, instead just use the infrastructure that is already available.
- It is up to the developer to create _great experiences_.

The Copilot Stack:

- Front-end, Orchestration, Foundation Models, and AI Infrastructure.
- FE: Plugin extensibility and UX.
- Mid-tier/Orchestration/Busines Logic: Prompt and Response Filtering, Metaprompt, Grounding (context, apis, vector DBs), and Plugin Execution.
- BE: Foundational Models (Hosted models, fine-tuned models, _Azure Models_, and BYO models), and AI Infrastructure.

Related Build Session: Building AI Solutions with Semantic Kernel

Copilot Media Provenance Tools:

- Watermarking capability.
- Helps protect your unique content.
- Supplied by Cryptographic APIs.

Q&A with Greg Brockman, President and Co-Founder OpenAI

- GPT3 had base model with basic training.
- GPT4 included deepter, instruction-following training.
- 'Boring engineering work' helped to develop a capable, effective tool.
- Build APIs to enable 'any developer' to builg their tools and context to the solution.
- Go into specific domains, understand pain-points, and apply ChatGPT APIs to help solve them.

Yusuf Mehdi expands on Copilot:

- Editing documents using Microsoft 365 Copilot with Office and plug-ins from companies like Thomsen-Reuters, Spotify, etc.
- Leverages Microsoft Graph.

Later:

Andrej Karpathy - The State of GPT (1445 to 1530)

Scott Guthrie Topics

- Every app will be AI powered.
- Building on Copilot Stack to demonstrate how it is used.
- VS and VSCode: Most widely used developer tools in the world.
- GitHub integrated end-to-end platform for collaboration, automation, and enterprise-ready service.
- GitHub Copilot: Pair-programming!
- Github Copilot X: Uses latest ChatGPT 4 models.
- OpenAI Uses GitHub for development.
- ChatPGT runs on Azure, and is backed with Azure Cosmos DB.
- AI Orchestration: So many Copilots built, using the exact same platform: Azure AI.
- Azure OpenAI Service: Newest GA service in January 2023, enabling ChatGPT and GPT-4 access. Find and fine-tune service instance data to build your service/plugin.
- Azure OpenAI Service instance data is isolated between customers/users.
- Azure AI Studio: Ground AI models w/ custom data and other details of Copilot building.
- Prompt Flow support in Azure AI: End-to-end dev tooling, experimentation, api, orchestration, testing, and deployment.
- Azure AI Content Safety: Test and evaluate AI deployments. Uses human and AI content. Provides severity scores to content.
- NVidia AI Enterprise: Will be integrated into Azure AI.
- NVidia Omniverse Cloud: Full stack environment for industrial metaverse _only_ via Azure AI.
- Microsoft Fabric: Unifies data, compute, experience, governance, and business models. Is a complete analytics platform, Copilot powered, and Microsoft 365 integrated. Now in Public Preview.

Thomas Dohmke talks about GitHub Copilot X, Copilot Chat:

- GitHub Copilot X - Copilot Chat
- Clean-up code to be readable.
- Add code comments.
- Find bugs in code.
- Add unittests to existing code.
- In preview by invitation (no release date given?).

Demo: Creating a ChatGPT Plugin

- Copilot Plugins are just web services!
- High integration with GitHub CodeSpaces.
- Enabling access to your API from ChatGPT _requires publicly available ports_.
- There are some imports necessary to enable building a Plugin.
- Utilize an Elastic Cloud service (Azure Kubernetes, etc) to
- GitHub Actions help with testing, building, and deploying Plugins.
- AZD can be used to build apps on Azure, leveraging templates, and automation (like GH Actions).

Demo: Building a Copilot

1. Create an Azure OpenAI Resource.
2. Configure with the desired GPT-n version.
3. Add Data Source following the RAG Pattern: Retreive facts, Add to the prompt, Generate new response.
4. Map indexing data together.
5. Set limiting responses to your own data only, or allow platform service enhanced data.
6. Open the Chat Playground and work with the Chat Session with your injected data included.

Demo: Prompt Flow

- End-to-end prompt engineering tool.
- Also monitors multiple sources and enable injecting into a prompt.
- Prompt Flow Graph: Flow data into the Prompt.
- Leverages APIs (demo used 'Minimal API').
- Prompt Flow provides logging, deployment, and configuration in one windowed view.

Azure AI Content Safety tidbits:

- Safety is key part to building any Copilot.
- Severity scores reject specific queries based on content.
- Even if a user has a history of low severity inputs, a higher severity scored input will still be rejected.
- Groundedness, Coherence, Relevance: Components of Copilot Safety that are scored, and can be viewed in Azure AI.

Microsoft Fabric:

- Use PowerBI Copolit to create reports based on specified data.
- Charts, slicers, etc are all automated by Copilot, repidly creating reports.
- Format report layout according to template designs.
- Manually change Charts and Maps as needed.
- Data refresh and filtering results are automatically updated on the created report.

## GitHub Copilot

Leslie Richardson Program Manager II, MSFT

GitHub Copilot is:

- Conversational AI pair-programming.
- Contextually aware.
- Describes what code in the working pane is.
- Code Completion suggestions.
- Scenario-based solutions to questions like 'how do I use method xyz?'.
- Drag-and-drop code using the Insert button.
- Code validation through Copilot-generated unit tests, based on 1 command.
- Will develop a service mock as needed in unittesting.

## Microsoft DevBox

Development environment with specified compute, storage, and dev-contextual features.

- Includes Visual Studio.
- Integrates with GitHub Copilot.
- Includes Azure Deployment Environments.
- Generally available.

### Azure Deployment Environments

Azure Deployment Environments, with Shayne Boyer Principal Progrma Manager, MSFT:

- GitOps!
- Cost free, except for the underlying resources utilized by each deployment.
- Platform engineering.
- Complete set of infrastructure tools for developing, testing, and deploying solutions.
- Create template dev environments for a team: Name, properties ram and compute, netowrk connectivity (such as location or local only), privileges for the user (standard user, administrator, etc), start/stop time with Time Zone context, and Licensing via Intune.
- Assign Roles and Subscription to tune the environment for the worker.
- Create isolated collections of infrastructure for PRs or other purposes, which will be automatically removed for e.g. when the PR is closed or merged in to target branch.

Now Generally Available.

## Selef Serve App Infrastructure Using Azure Deployment Environments

Presenters

- Sagar Chandra Reddy Lankala, Sr Product Manager MSFT
- Jared Rewerts, Software Engineer MSFT

SDL Transformations

- DevOps transformed software development lifecycle.
- DevOps requires Developers to concentrate on infrastructure.
- Administrators (experts in infrastructure) help supply, deploy infra.
- Challenges with mundane work and managing costs and auditing usage.

Cloud Based Infra Imperatives

- Speed: Performance must meet demands, requirements of the project(s) that depend on it.
- Governance: Maintain centralized control.
- Usability: Infra must be configurable, manageable, else it might as well not be there.

Azure Deployment Environments

- Developer-centric Self-Serve, standardized Templates.
- More than 30 Enterprise customer provided feedback to this since last year.
- ADE is now GA.
- Currently native with GitHub.
- Can be extended to use other repository types.

Maximize Developer Productivity

- Self service access to On-demand templates.
- Environments within project-specific template catalogs.
- Deploy direct from code repo, CLI, or Dev Portal.
- Sandbox, On-demand, and CI/CD Pipeline Environments, all driven by Dev Poetal & Dev Tools, or Pipelines for Enterprise.

Demo: New Developer Ramp-up Time

- Review the project infrastructure/overview to understand the complexity, moving parts, etc at a high level.
- Newbie wants a breakable environment, using the target environments, without negatively impacting customers, other developers, etc.
- Utilize Developer Portal to display DevBox template environments and create new ones.
- Select an Environment Definition. Think of these as 'infrastructure as code' that stands-up necessary bits to support the environment.
- Additional Template parameters might be necessary (or not).
- Once deployed, developer is ready to get started developing, testing, etc.

Demo: Dev Environment For Development

- Sign-in to DevBox.
- Open VSCode (web view) to view the code.
- Make changes and push changes to GitHub.
- Actions are fired upon Push that create the deployment environment along with logs.
- Creating a PR spins-up _another environment_ for PR Review, specifically.
- Various environments build-up in branches and Dev Environment deployments, which will be depeted upon other tasks.
- With PR Approvals and Merge-in, Dev Environments related to the workflow stages are deleted, freeing resources, and limiting costs.

Demo: Platform Engineers Create Dev Centers

- Maintain and control access to Dev Environments for the organization.
- Catalogs: Source infrastructure templates. Simply uses a Clone URL.
- Environment Types: Roughly equivalent to a developer team. Attached to deployment subscription(s), deployment identities (who is deploying the environment), and access levels e.g. Active Directory groups.
- Tags: Name-Value pairs to help identify deployments. Bubble _down_ to the _environment_ level, for search and reporting.

Coming soon: Azure Developer CLI (AZD) + Azure Deployment Environments.

## Resources

Code for Kevin's PodCast Copilot [github.com/microsoft/PodcastCopilot](github.com/microsoft/PodcastCopilot).

Coding Java using Azure tools [aka.ms/java-azure](aka.ms/java-azure).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
