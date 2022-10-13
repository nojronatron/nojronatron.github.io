# MS Ignite Octoboer 2022

## Pre-keynote

Unprecedented times, uncertain times, technology is the way forward!

Resiliency: How you manage when bad things happen to you.

Two Clouds: Industry, and for Sustainability.

Ignite Themes:

1. Be data driven, optimize with Azure
2. Delivery efficiency with automation and AI
3. Innovate with a cloud developer platform
4. Re-energize your workforce with Microsoft 365
5. Protect everything, everyone, everywhere

## Keynote

Satya Nadella - MSFT Chairman and CEO

Orgs in industry are turning to devs and techs to be change agents through these challenging times.

Harder, longer working does not scale. Applying technology to do more work *does scale*.

Infrastructure Layer:

- Where everything starts.
- Moving to cloud allows scaling with demands.
- SQL and VM's highlighted as the best way to meet increasing demands.

Data Driven, optimize with Azure:

- Azure Arc: Build app with Azure Services, Kubernetes enabling IoT, Edge, Servers, etc.
- Ampere Ultra ARM-based processors now available in Azure.
- Premium SSD v2 Disk Storage.
- Azure Elastic SAN: Cloud-native, fully managed storage area network service.
- Azure confidential computing protects data at Rest, in Transit, while in Use. AMD, Intel, and nVidia involved. Applies to VDA, SQL, and ?
- Azure Cosmos DB supports NoSQL + Relational Data.
- MSFT Purview: Unified data governance and data security and privacy.

Deliver efficiency with automation and AI:

- Azure Machine Learning: Build, train, deploy large AI models at scale.
- Azure Container for PyTorch: Optimized Training and Inferencing engine support.
- Supported models: Turing, Z-Code, Flourence; GPT, DALL*e, Codex.

Codex demoed "pair programming" capability where a user enters a problem, and Codex correctly codes a solution. It took several tries, but Codex discovered its own bugs and fixed them.

- There was no discussion on efficiency of the algorithm in part or in whole.
- Codex was able to correctly import the Random module for use in the solution attempts.

Innovating with the Most Comprehensive Cloud Platform

- GitHub co-pilot: Finishes lines of code the dev starts, and even suggests functions for the problem at hand.
- AI Builder enhancements in Power Platform (lots listed, too rapidly to record here).
- MSFT Syntex: Content AI and process automation, including classification and annotation capabilities -- translation tool.

Re-energize the Workforce using Microsoft 365

- There is no going back to 2019!
- Three prioritization: Stop endless work paranoia; People come to the office to socialize, not for policy; Skill building and education must be a part of the investment in employees.
- Microsoft 365: Microsoft Graph underlying all MS365 products. New products added to the collection.
- Teams: Sync/Async collaboration is a requirement for performance and effectiveness. Whether together or away, both collaboration types are necessary. Building Apps for Teams has become a thing! Cisco Rooms natively supports Teams now. Mesh Avatars coming to Teams. Integration with Meta?
- New: Microsoft Places, part of the Teams family?, due in 2023.
- MSFT Viva: C-level data, CRM-data, and other info for executives? Satya hinted this will be extended to many other worker roles.
- Edge Workspaces: Shares tabs across users - multi-player web browsing.

Protect everything, and everyone, everywhere:

- Risk management becomes more difficult as the complexity of the system increases.
- Entra, Purview (compliance, data govnance); Priva, Intune, Defender, Sentinel.
- Implmentation extended to all clouds and environments.

## Build Agility, Drive Innovation With The Cloud

Scott Guthrie and Alysa Taylor

Use lowcode and nocode tools to democratize technology to as many people as possible.

Example: Reduce actual labor hours building solutions to automate some or most of that effort using lowcode/nocode tools.

Technology helps workers process and work with data to complete tasks and meet business goals. Adding AI can reduce friction (and time) to process completion.

## Industrial Metaverse

In a nutshell, design, build, and test industrial systems without laying a single brick.

By avoiding building until bugs are worked out, expected and unexpected costs can be reduced, and impacts on teh environment are reduced.

## Low- and Pro-code Tools

Speakers:

- Charles Lamanna, MSFT Corp VP Business Apps & Platform
- Donovan Brown, MSFT Partner Program Manager in Azure CTO Incubator

MS Cloud Developer Platform

- GitHub Codespaces: Full dev environment in-browser from a GitHub repository.
- GitHub CoPilot: AI Pair Programming.
- Azure DevOps
- GitHub Advanced Security for AzureDevOps: Secret, dependency, and code scanning, blocking shared creds into source control. Integrates with Defender for Cloud.
- Azure Kubernetes: Scale cloud-native applications.
- Azure Kubernetes Fleet Manager: Multi-cluster workload and services management layer.
- Azure Container Apps: Built on Kubernetes, supporting code dev.
- Power Platform: Use a connector (published API) to connect to existing dev environment.
- Power Platform Managed Environments: Enable IT to manage low-code Apps (now GA). Control app lifecycle, flows, env publishing, policies, and licensing.
- MS Dev Box: Dev VM in the cloud.
- Azure Deployment Environments: Infrastructure in the cloud for dev and text deployments.
- Azure CosmosDB: Developer-oriented db with NoSql support.
- Azure AI: Vision, speech, language, and decision-making AI models via simple API calls. Integrates with Jupyter Notebooks, VS Code, TensorFlow, PyTorch, and other open-source frameworks.
- Azure ML: Basic or advanced service solutions.
- Azure LogicApps: Create workflows to automate feature development and deployment work.

## Re-energizing the Workforce

Presenters:

- Jared Spataro, MSFT Corp VP  of Modern Work
- Caroline Stanford - MSFT Dir of Product Marketing Microsoft Teams

Focus is on Microsoft 365 applications and features.

- Productivity Paranoia: Leaders are not sure employees are being as productive as they could be.
- People come to the office when it is worth the commute to be social with their teammates. Completing tasks can happen *anywhere*.

Microsoft 365 App:

- All existing tools.
- Backed by MSFT Graph.

MSFT Graph:

- Relationships in content between Apps are presented within each App view.
- Feed feature collects data and events into a schedule and day-viewer.

Teams:

- Remote, in person.
- Synchronous and Asynchronous productivity.
- Support to edit app data within Teams, without opening the App separately.
- Premium version now GA.
- Intelligent Recap: AI-assigned tasks during meetings, calls out important moments in meetings, and 40-launguage captioning.

MSFT Designer

- Uses AI to turn descriptions into web/publishable pages.

Viva

- Released last year.
- Aligns employees around organizational goals and mission.
- Built-in to Teams and Outlook.
- Includes learning portal for skill building.
- A communications channel.
- Has social publishing capabilities e.g. employee blogs etc.

MSFT Places

- Help organize spaces for when employees come in to the office.
- Enables collaborating in and out of the office.
- Generate statistics on office space usage.

Meta + MSFT

- MS Teams integration into Meta Quest.
- MS Teams meta avatars.

Windows Desktop

- Windows 365: Build PC in cloud and stream it to *any device*.

## Sysinternals Tools Overview

Mark Russinovich and Scott Hanselman

SysInternals tools is over 26 years old and running!

There are a few SysInternals tools that are now available on linux!

ZoomIt was the target pair-programming session code!

Resource Editor: Allows viewing hexcode of executables.

Process Monitor: aka procmon. 'When in doubt, procmon'.

- Windows doesn't have to be a blackbox.
- SysInternals bring all that blackbox stuff into the forefront.
- View how an executable was launched!
- See the result of method calls in the binary itself.

Pen and Touch Input was added in 2015!

- There was a bug that was caused by an uninitialized variable. :astonished:

Mark Russinovich:

- No SysInternals source control until 2007. They used to pass around a zip file between developers!
- "I am the unit tester". :astonished:
- Running in Debug mode will crash (the type left-shift feature done live) due to off-screen boolean test. In Release mode the App won't crash because the false return (in a character printing library). As a developer, this type of thing is good to be aware of.
- Anytime these tool(s) are wanted, just go to WebDAV site `\\live.sysinternals.com` and xcopy/download what is needed!
- Linters *can not* catch all of the memory management issues.
- Rust is a great alternative to C/C++. The goal of Rust is to avoid coding issues related to memory e.g. local uninitialized variables.

Scott Hanselman: Agressive-refresh is available is Chrome! Open DevTools then rClick the refresh button.

- Normal Reload.
- Hard Reload.
- Empty Cache *and* Hard Reload.

Individual SysInternals tools can be downloaded direct from internet file share :boom:`\\live.systeminternals.com`:boom:.

## Live Demoing ASP.NET Core and DotNET 7

Presenters:

- Damian Edwards, MSFT Principal PM Architect
- David Fowler, MSFT Parner Software Architect

'builder.Services' can have policies added in custom methods. E.g.: Custom rate-limiting.

Custom cookies: Can be used to partition policies (limiters in the example they were showing). This can make it so that different sessions do not count toward each other. For rate-limiters, that means each session is rate-limited individually.

Target-type 'new': C#11. If the type is already known, or the assignment is to a previously typed variable. E.g. `new() { props... }`, very much like JS Object Literal syntax.

RequestLogging:

- Usually coders buffer the request, gather all the info and stream it to the log, and also allow the request to get processed by the system.
- Coders also do a lot of dancing with responses as well, just to get the response logged.
- It is difficult to get these right as in: Stable, Secure, manages private data properly, and is Performant.
- Also, streaming very large requests can be tricky or possibly dangerous to the health of the server.

Better RequestLogging:

- New feature `builder.Services.AddHttpLogging(()=>{});` from `useHttpLogging()`.
- Leverages the WebApplicationBuilder middleware.
- Captures Req and Res bodies!
- Large Req and Res data is truncated so they don't overload the logfile(s).
- Sounds like: Redacting private/secret data is done by default.
- Log output format is MSFT standard so most log scrapers should be able to parse it natively.

Output Cache

- ResponseCaching allows devs to change caching behavior so a web element can force the browser to update a cached response. Browser refresh will still use local cache.
- OuputCaching can be applied to endpoints directly, or by policy by defining rules and then apply them to things 'by name'.
- Basically, cache handling is determined by the browser, the http server, and headers, and these two DotNET middleware libraries allow managing these easily.

UseStatusCodePages

- Formats status code pages for you.

UseExceptionHandler

- Used to have to implement what happens when an exception is thrown.
- With this, a safe throw return is provided to the client!

CustomizedProblemDetails

- Method group that will allow setting a delegate via Options to define what the dev wants/needs.
- Live-code implementation demonstrated adding a custom property.

Startup Hooks

- Set an env variable for your process to point to a dll before main runs!
- Class has to be top-level with a public static entrypoint named `Initialize()`. Unclear if void return is required.
- Configure launchSettings.json to point to DOTNET_STARTUP_HOOKS to point to the dll to call.

DotNET Native AoT

- Compile dotNet app down to a small, native executable.
- AoT *uses* trimming.
- Trimming removes the JIT and lots of added code cruft, so only the core, necessary services are included.
- Check out Damian's [TrimmedToDo repo in GitHub](https://github.com/DamianEdwards/TrimmedTodo).

## Windows: Building what matters

Panos Paney Ex VP and Chief Product Officer hosts Windows Team leaders with discussion around Windows 11, new Surface Hardware, and Windows 365.

Windows 365:

- Cloud PC => Switch to Windows 365 desktop *from your current desktop*.
- Downloadable as an App now, later will come with Windows 11.

Security and Development and Devices:

- Zero Trust.
- Software and hardware security protections.
- Secure Core :tm: PCs.

Windows 11:

- Protects user from sending credentials to an unusual or unexpected service.
- Very high app compatibility and AppAssure to help resolve many common compatibility issues.

## Inside Azure Innovations

Speaker: Mark Russinovich

200 datacenters with many more per year around the globe.

Many of the following features and capabilities are not yet released - 'coming soon'.

Cooling:

- Air-cooled and liquid-cooled infrastructure is employed.
- Typical server dissipates ~350W, so higher density can only be reached with liquid cooling.
- Two-phase Immersion Cooling reduces failure rate, and no water in the system.

Patching and fixups:

- Hot Patch: Minor fixes but fast
- Microcode updates: Reboot-less firmware updates!
- Hypervisor hot restart: Enables installing new features w/o downtime. *Hypervisor state* is transfered from one server to another.

Accelerated Offload Processing:

- FPGA for programmable networking, storage IO.
- SoC runs Linux to do be a management plane.
- Free-up CPU load from handling IOs to data processing instead.

Accelerated Networking with Serius Appliance:

- Extreme performance VMs move to specific appliances.
- Extreme performance network equipment host these higher requirement VMs.
- Saves from having to install extreme-performance offloading equipment to every server in every rack.

Offloading Block Storage:

- SAN performance and management in the Cloud.
- Azure Elastic SAN provides public cloud SAN (Volume groups, Volumes, Azure Storage).
- Azure Storage is striped across many devices to increase overall bandwith.
- SCSI devices projected into the VMs allowing SCSI performance.

Containerization is the Future of the Cloud and Enterprise:

- Serverless containerization, specifically.
- Define an App, with container specs, give to public cloud, and let it run.
- Azure Container Instances (ACI Service) allows creating many containers quickly. Scale up/down rapidly, over and over.
- Containers are more rapid than full virtual machines, but groups of them require time to launch. Warm Pooling pre-warms containers.

Confidential Computing:

- Evolved from encrypting at rest data with keys, protecting data in transit via SSL + TLS.
- Now protect data *in use*.
- Hardware with encrypted memory, disallows anything outside the harware from getting access into the box.
- Hashed code and policy comparisons are run to determine trusted services, and allow data transfer.
- Mark mentioned [Confidential Computing Consortium](https://confidentialcomputing.io/) (also see Open Enclave SDK by MSFT).
- Mark demoed protecting data sent to an ML Model on the public Azure cloud.
- Azure KeyVault stores the keys, with new mHSM feature.

Quantum Computing:

- Mark overviewed existing capability and challenges with quantum qBit types.
- Topological qubits: More stable, non-sized, fast qubits that might solve the 'million qubit problem'.
- Too much deep stuff to document here, so in summary MSFT has tested a design that is the basis for a topological qubit, so work is well underway.

GP Servers:

- Customers were bringing very large workloads, especially database workloads, so MSFT built larger servers to try and meet the needs.

## Supporting and Executing Remove Development

Hardware:

- Remote developers work on laptops received in the mail or their own equipment.
- Might not have IT secure packages at all, or that work well with developer workstation environment.

Dev Environments:

- Could be local only, where projects could pollute each other.
- Could be virtual/cloud based development, putting additional requirements on processing and network resources.

Microsoft Dev Box:

- Deploy and use Windows 11 desktops
- OneDrive document synchronization.
- Azure Deployment Environments provides services needed to work.
- Removes processing from local workstation/laptop - all processing for build, debug, etc happen on the remote desktop in Azure.

MS Dev Box with Maui:

- Multi-platform build and deploy capabilities.
- Simplified Project File for framework and architecture targeting.
- Auto-scaling of svg files for mobile and desktop.
- XAML Live Preview: Like DevTools in Chrome, Elements tab.
- XAML Hot Reload: Changes in code are displayed in Live Preview.
- Data Binding Diagnostics: Helps locate misspelled or misdirected data bindings.
- Live Visual Tree: Tree view of XAML Live Preview.
- Debug Android version of app: Within VS, or *on an Android emulator*.
- Dev Tunnels: Private vpn-tunnel allows serving debug-mode code to remote devices including browsers and mobile.
- VS now has markdown highlighting/linting, as well as live-preview.
- Load Testing available in an isolated Azure environment (Deployment Environments).

DevBox

- Full machine for whatever dev environment including VSCode and Visual Studio.
- Fully sandboxed.
- Base images with pre-installed VS instances available.

Azure Deployment Environments

- Enables devs to deploy environments w/o subscription access.
- Use template(s) to spin-up resources for the project.
- Infrastructure-as-Code templates: Stored in GitHub repos as ARM Templates.
- Yaml used to configure deployment.
- Catalogs are created and made available to devs as deployment targets.

## Footer

Return to [conted-index.md](./conted-index.html)
