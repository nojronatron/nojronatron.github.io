# MSBuild 2024 Notes

Microsoft Build is a yearly conference aimed at .NET developers and focuses on Visual Studio, languages like C#, F#, and Visual Basic, developing solutions using Azure or Microsoft 365, and updated information on .NET.

MSBuild takes place on 21 May through 23 May, 2024.

## Table of Contents

- [Keynote - Wednesday](#keynote---wednesday)
- [Extend Microsoft Copilot Using Copilot Studio](#extend-microsoft-copilot-using-copilot-studio)
- [Maximize Joy Minimize Toil With Greater Dev Experiences](#maximize-joy-minimize-toil-with-greater-dev-experiences)
- [AI Everywhere Breakout Session](#ai-everywhere-breakout-session)
- [Imagine Cup Finals](#imagine-cup-finals)
- [Keynote - Tuesday](#keynote---tuesday)
- [Resources](#resources)
- [Footer](#footer)

## Keynote - Wednesday

Speakers: (tbd)

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

[Windows Developer Center](https://developer.microsoft.com/en-us/windows/).

[AI Toolkit for Visual Studio Code](https://learn.microsoft.com/en-us/windows/ai/toolkit/) Overview (previously named "Windows AI Studio").

SLM: [Small Language Model](https://news.microsoft.com/source/features/ai/the-phi-3-small-language-models-with-big-potential/).

[Phi-3 SLM](https://azure.microsoft.com/en-us/blog/introducing-phi-3-redefining-whats-possible-with-slms/).

[Mistral SLM](https://mistral.ai/).

[ONNX Runtime](https://onnxruntime.ai/blogs/accelerating-phi-3) supports Phi-3 minim models across platforms and devices.

Direct Machine Learning [DirectML Overview](https://learn.microsoft.com/en-us/windows/ai/directml/dml): A low-level API that requires DirectX 12-compatible hardware.

[Microsoft 365 Blog article](https://www.microsoft.com/en-us/microsoft-365/blog/2024/05/21/new-agent-capabilities-in-microsoft-copilot-unlock-business-value/) about Microsoft Copilot's new capabilities.

[Intel Accelerator Engines and Intel AMX](https://www.intel.com/content/www/us/en/products/docs/accelerator-engines/what-is-intel-amx.html).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
