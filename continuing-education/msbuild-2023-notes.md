# Microsoft Build 2023 Notes

Twitter: @msdev, #MSBuild

Official [Build Playlist (Spotify)](aka.ms/buildplaylist)

## Table of Contents

- [Keynote](#keynote)
- [GitHub Copilot](#github-copilot)
- [Microsoft DevBox](#microsoft-devbox)
- [Self Serve App Infrastructure Using Azure Deployment Environments](#self-serve-app-infrastructure-using-azure-deployment-environments)
- [Shaping the Future of Work with AI](#shaping-the-future-of-work-with-ai)
- [Dev Joy with Scott Hanselman and Friends](#dev-joy-with-scott-hanselman-and-friends)
- [Open QA About Java at Microsoft](#open-qa-about-java-at-microsoft)
- [Just Say No](#just-say-no)
- [Resources](#resources)
- [Footer](#footer)

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

- Bringing Bing to ChatGPT.
- Windows Copilot: ChatGPT will help configure Windows for productivity and focus, as well as integrate with other Microsoft tools e.g. Microsoft 365, Office, etc.
- Copilot Stack: Apps, Orchestration, and Models and AI Infrastructure
- Azure AI Studio with Azure AI Safety: Testing, Governance, Deployment.
- Microsoft Fabric: Data analytics for the era of AI.

Build with safety first (more about this later).

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

## Self Serve App Infrastructure Using Azure Deployment Environments

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

## Shaping the Future of Work with AI

Tuesday morning Keynote

Presenters:

- Rajesh Jha, EVP Experiences, Microsoft
- Panos Panay

### Overview

- Democratize the opportunities for developers to utilize AI, making it accessible around the world.
- AI is the new frontier of computing, much like GUI's were 30 years ago.
- Survey indicates 2 of 5 days a week were spent coordinating vs other productive activities.
- 1 Billion people using Windows daily. 100 Million people using Bing daily.

Jon Editorial:

- MSFT Teams is becoming its own ecosystem with hundreds of thousand of commercial and custom apps.

### Copilot Stack

Microsoft 365 Copilot:

- Runs on top of foundation models running in Azure.
- Includes Microsoft Graph, as the context of the User (grounding the AI).
- Cross-app and In-app capabilities: Context to content and workflows revolving around the user.
- Copilot acts on the users behalf, using ChatGPT plugins standards.
- Copilot Plugins will work across the Copilot ecosystem (Bing, Microsoft 365, etc).
- Connections between apps and services represent Copilot skills.
- Teams Toolkit: Enable build, debug, and deploy plugins.

#### Build Copilot Plugin Extention

Demo Presenter: Archana Saseetharan Prin GPM, Microsoft

- Used VS Code.
- Swagger UI used to review and explore the Copilot Endpoints.
- Run-and-Debug tool enabled to find what code was running when an Endpoint was hit.
- Plugins support anonymous access AND authentication (as defined in the Manifest).

Create Plugin for Copilot:

1. New Project
2. Plugin for Copilot
3. Select methods in API to expose to the plugin
4. Add project folder and name
5. Side-load the plugin in VSCode to view execution

Key Components:

- Manifest file: Defines basic metadata of the plugin.
- Adapter cards (as in Boostrap Card UI element).

Helping Developers Build AI-integrated Apps:

- Productivity: Enable users to simply interact with data, context, events, and resoruces.
- Reach: App compliance, M365 certification, Discovery and deployment of apps, auto-installation.
- Discovery: How Consistent store experiences within M365, Discoveraly in-flow of working, Contextual access in Teams Chats, channels, and meetings. Ensure the correct App surfaces in the correct situations.
- Revenue/monetization: Commercial marketplace for regional, department, or global level. Includes license management.

Jon Summary:

- Plugin creation completed within 5 minutes.
- Obviously, some API endpoints already existed for the demo, but adding the Copilot functionality was pretty simple.

#### Cross-App Capabilities

Demo Presenter: Archana Saseetharan Prin GPM, Microsoft

- MSFT Teams integration with Copilot.
- Copilot could find Emails, read attachments, and make suggestions based on those inputs.

#### MSFT Graph and Semantic Index

- This gets built and reorganized every day from inputs generated by users.
- Graphs are segregated by multi-tenancy.
- Access and Permissions are applied _by user_.
- All interaction with User and AI is not treated differently than usual interactions.

Semantic Index:

- A Vector Index.
- Represents relationships between users, events, and resources.
- Part of the inputs into the AI as part of its Grounding.

Demo: Semantic Plugins

Presenter: Yina Arenas, Partner GPM Microsoft Graph, Microsoft

- Copilot integration with Jira Cloud, brought in information from the current context, creating a new 'ticket'.
- OpenAI standards or Messaging Service standards can be followed to plugin to Semantic Index.
- Users' intent is surmized using Graph/Semantic Index, within the Apps the user in interacting with.

Demo: Integrating with copilot

Presenter: Wamwitha Love, Prin PM Manager, M365 Platform, Microsoft

- All actions done within Teams (calls, video, and chats).
- Using information gathered, copilot generates a document for the user.
- Copilot can be prompted for additional details and prompts user to allow adding data into the document.
- Copilot processes conversations, and prompts user to allow gathering additional information on the topic (in this case, customer and competitor information, during a meeting to form a proposal).
- Documents can be saved to the connected CRM after updates.
- Document editing and updating can be assisted, and completed, using the Copilot plugin(s). This part of the demo was showing a draft legal document and Copilot plugin was asked to remove a specific paragraph from the document.

### Teams Live Share

Applications and docuemnts should be collaborated on during meetings.

Features:

- Live App collaboration in meetings.
- Co-create, co-watch, and co-edit.
- No backed code required.
- Released NOW.

### Microsoft Mesh

Features:

- Personalized Avatars for MSFT Teams.
- Immersive spaces in teams.
- Extend ANY TEAMS MEETING into an immersive experience.
- Build templates for immersive meetings.

Jon Commentary:

- Similar to Metaverse, built to use on Teams.
- Still no legs?

### Windows Copilot

Presenter: Panos Panay EVP, Chief Product Officer, Microsoft.

- Replayed Satya's presentation video on Windows Copilot: Centralized AI assistant; Configuration settings assistance; Explain, Rewrite, Summarize docuemntas; Find and play music; Plugins add to your workflow within Windows.
- "I need to cast my screen to my TV", and it just happens via Windows Copilot.
- Windows Copilot offers 'desktop cleanup', to _help you stay productive_.
- When copying text, Windows Copilot can ask what to do with the text. :tada:
- Drag-and-drop audio files to Copilot and tell it what to do: Transcribe it, listen to it, edit it, etc.
- Preview in June 2023.
- Windows 11 is nearly 2 years old (from announcement to today).

### Dev Home

- Signin to GitHub, get access to apps and repositories.
- DevDrive natively tracks changes with Git.
- Dashboards to view repos and project status, motion.
- Direct access to VSCode and GH Copilot.

### Powertoys on AI

Presenter: Shilpa Ranganathan, CVP MSFT Product ??, MSFT

- Developers were right when they said Powertoys is necessary for setting up dev environment on Windows.
- Dev Home: Setup GitHub, Install necessary tools and packages.
- Synchronization between File Explorer, Windows Terminal, etc.
- WinGetConfig: Define a dev enviornment in a config file and apply it to your system.
- Dashboard: Glancable overview of dev environment state, CI Status, Task Tracking Widgets, and is _extensible_.
- DevHome is an OSS tool!
- MS Store has DevHome in Preview today.
- GitHub Copilot X for Windows Terminal! (get on the waitlist)
- The Widget Board, introduced in February 2023, upgraded today. Features: Quick, glance-able content.
- App Restore: Move apps from old box to new! In preview for Insiders.
- Windows Subsystem for Android was mentioned, but no details.
- AI Hub (MS Store): Showcase best of AI Applications.

### AI For Every Developer

Presenter: Pavan Davuluri, CVP ... MSFT

- Windows AI Libraries: Coming soon! Windows 11 has AI Models built-in to get started quickly.
- ONINX Runtime: Targets existing AI Developers. Camo is an example.
- Hybrid Loop: Enables running models locally AND in the cloud.
- Olive Toolchain

Camo:

- Spotlight
- Autoframing
- Privacy mode
- Overlays
- Producing videos
- Works with any existing video/web cam
- Is an AR integrated video tool
- Can add hand gestures to live video
- Comming to Windows 11 soon

Partnership with NVidia: MSFT working with NVidia to pro

NPUs

- ML and AI focused processors.
- Intel developing 'neural processors'.
- Qualcomm Snapdragon platform updates.

### AI Changes Everything

Presenter Steven Bathiche, Tech fellow W + D, MSFT

- Windows, M365, and Azure ML: Single-click model adjustments.
- Contextualize every interaction: Ground the API at every prompt.
- AI Is The New Interaction Technology: Keyboard and Mouse is over 50 years old, and AI is the next interactive interface breakthrough.

Infusing AI into experiences:

- Beside: Add Copilots to help complete tasks.
- Inside: Create Apps with AI at the core. Redefine interaction, away from point-and-click, and into automated interactions.
- Outside: Agents orchestrate across apps and tasks.

Note: Windows Terminal can be used as an Orchestrator.

#### Oninx Runtime and Olive Toolchain

Cassie Vreviu, Sr. ??? MSFT

- Does heavy lifting for developers.
- Used within Microsoft developer teams for creating internal tools and commercial apps.
- Olive automates workflows (targeting data scientists, AI-centric developers).
- Demo: Use Olive to optimize AI Model(s). Note: WPF Application was called-out in this demo!

#### MSFT Syntex Plugin

AI Tool that enables classification and tools to unlock AI capabilities to enable business processes to be grounded in the users context.

- Build documents from 'structured templates'.
- Document review including detail spotlighting.
- E-Signature highlighting and signing via Copilot.

## Dev Joy with Scott Hanselman and Friends

Developer Joy VS Developer Toil

- OOBE: Deploying 'the new box'!
- WinGet for simple setup.
- Developer Home: Repo management, and coding inner-loop speed.

Developer Inner Loop:

- Code
- Build
- Test
- Deploy
- Repeat

Outside the Inner Loop:

- Push container to a registry
- Deploy the code
- Governance
- Etc

General Notes:

- VSCode Icon was added to the Windows OOBE login page.
- WSA: Windows Subsystem for Android!!
- OOBE now includes a "Developer" experience checkbox. This deploys DevHome to your system to be ready once at the desktop.
- Winget: Develop a YAML DSC file to get the desired packages deployed more rapidly.
- Launch File Explorer from the Terminal: `start .`
- Terminal is more customizable than before and supports USB-Drive execution.
- Terminal Tab Tearoff enables removing a Tab from host Window into a new Window.
- Terminal supports Windows 10 too!
- Winget Configure, DevHome, DevDrives: Enabled (and soon) in the cloud.
- DevHome: Develop a YAML file, check it in to your GitHub repository, and DevHome can use that as a guide to ensure prerequisite software is installed.
- DevHome: DSC/YAML will also allow DevHome to manage _software that you do not want_ e.g. Ensure the correct version of Node is installed.
- DevHome: Supports GitHub, Azure DevOps, PowerPlatform, and more.

## Open QA About Java at Microsoft

Java Binaries, Licensing, and the open-source JDK:

- Usually the OSS JDK fits the need.
- For specific scenarios, looking at costs for licensing will be an exercise for the team or organization.

Copilot and Java:

- Works well with Java code.
- Occasionally comes up with proposing methods and tests.
- Worst case scenario it is coming up with something that can be edited to 'be what you were looking for'.
- IntelliJ has a Copilot plugin for IDEA.

Azure Functions vs Services:

- Consider how often a function is being called/spun-up.
- Azure Functions are ephemeral, short-duration tools.
- Azure Functions supports newer Java versions, possibly as far back as Java 8.
- Kubernetes containers might be a good option for longer duration or more busy function execution.
- A full-on Azure Service would be recommended for an on-going, regularly executing function.
- Azure Functions can be used as a trigger to cause a workload in another environment to execute.

Java Version Usage:

- Current LTS Java versions are 11 and 17.
- Next LTS Java will be 21.
- LTS versions are supported for about 6 years ("until at least").
- Quarterly LTS updates.
- MSFT assists in development and maintenance of Eclipse Adoptium Binaries.
- MSFT utilizes Java 17 for all unit and functional testing.

MSFT Spring Framework Support:

- MSFT is partnered with VMWare (prior to acquisition of/by Pivotal).
- Spring Boot and Spring Could Libraries are well supported at MSFT.
- Cloud, Security, and other umbrella projects are supported end-to-end.
- Spring Boot support is in Azure.
- Spring Framework holds something like 70% of the Java Framework ecosystem.

WSL2 and VSCode and Developing Java Apps:

- Selecting Runtimes and JDKs and default runners.
- WSL2 requires installing JDK and CLI etc, Gradle, Maven, etc.

Advice for Teams Migrating from DotNET to Java:

- Don't create methods with a capital letter! :smiley:
- Get acquainted with the Java ecosystem.
- There are many different implementations, not one is 'perfect'.
- Pick one that looks good enough (or easy enough) and start working with it.
- MSFT DotNET has fed knowledge into the Java ecosystem.
- Dependency management differs from the DotNET world (Gradle and Maven).

Java vs Kotlin vs Scala decision making framework?

- About Scala: Is not 'fully interoperable' with Java, but has declining interest and support.
- Kotlin 'felt like the future' vs Java being a bit older (long in tooth).
- Gap between Kotlin and Java is closing.
- Kotlin and Java compile-down to the same bit code, so mix-and-match is an option.
- Kotlin is 1st-class in IntelliJ (Kotlin is developed by JetBrains) but not in VSCode.

## Just Say No

Host: Debbie O'Brien
Co-host: Scott Hanselman
Moderator: Justin Yoo

General Notes:

- When a new opportunity comes to you, is it difficult to say no?
- Are you just trying to be a people pleaser?
- A mix of imposter syndrome and fear of missing out can drive to YES when NO might be better.
- Burning out can result. Debbie ended up in the Hospital due to stress and overwork.
- Try this: Put a timer on allowing the emotions to roll and be in the moment to help get through tough times.
- Do more of what makes you happy. Is what my manager is telling me to do going to make me happy?
- Applying color labels to work items, calendar items... helps you prepare for scheduled items that are happy/good, and prepare for those that require additional preparation/work.
- Put one-on-one meetings in my calendar (but don't invite anyone): Plan for the week early on, then on Friday look back and forgive what hasn't been done or for actions taken, but leave that meeting and its contents in the meeting. Plan, and then release.
- Don't sleepwalk through your career. Wake up by deciding what goals to meet and when, and do things that support making that goal.
- Setting boundaries: Set a specific "end of day" time and turn-off all applications (unless you have agreed to be 'on call').
- You have the power to teach your boss how to treat you. For example: If you respond after your boundary 'not working time', you are opening the door to continued access at that time. Another example: It is important to talk to your manager about how you want to be managed, and what will wrk for you.
- Resentment comes from unmet expectations. Unspoken expectations leads to resentment.
- Expect a 60 hr week to be followed with a much shorter work week. If that cannot be met then a conversation must take place so that expectations can be reset between manager and employee.
- Come to the table looking for a win-win agreement.
- Prepare to set a 'core hours' timespan where you will be 'in the office/totally available'. This doesn't mean only work those hours, rather these are times when most interactivity and productivity is going to happen. Working outside of those hours is up to each individual.
- How to say 'no' though? If the question is not a 'heck yes!' then it might be a no. Otherwise, discuss the requirements and priorities to come to an agreement as to what could work.
- It is good practice to write-out a list of 'no' responses _that include the why_, along with appreciation in your response. Also, if the budget doesn't meet the ask, or otherwise does not align with previous agreements and/or your goals, it should be discussed or considered a strong 'no' with appreciation.
- Strangers asking you to do something might not even require a response, it depends on the situation. It would be considered very kind to respond in any way, however a non-response is usually forgotten and/or excused.
- Which mountain (of code languages, frameworks, etc) do I want to focus on? Nobody can do them all. "You can always click unsubscribe" to whatever you are doing. _[Scott Hanselman]_
- Everyday, compare yourself _only to yourself_ and nobody else.
- Work hard, then _take a break_. So long as you are enjoying yourself, keep it up!

## Resources

Code for Kevin's PodCast Copilot [github.com/microsoft/PodcastCopilot](github.com/microsoft/PodcastCopilot).

Coding Java using Azure tools [aka.ms/java-azure](aka.ms/java-azure).

Learn more about MS Build 2023 topics at [aka.ms/LearnAtBuild](https://aka.ms/LearnAtBuild).

Check out [aka.ms/java-azure](https://aka.ms/java-azure).

Check out [Java on Microsoft portal](https://developer.microsoft.com/java).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
