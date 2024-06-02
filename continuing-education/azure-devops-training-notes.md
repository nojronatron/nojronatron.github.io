# Azure Dev-Ops Training Notes

## Table of Contents

- [Working With Azure Repos and GitHub](#working-with-azure-repos-and-github)
- [Choosing DevOps Tools: Azure and GitHub](#choosing-devops-tools-azure-and-github)
- [Assess Your Development Process](#assess-your-development-process)
- [What is Azure DevOps](#what-is-azure-devops)
- [Azure Pipelines](#azure-pipelines)
- [Resources](#resources)
- [Footer](#footer)

## Working With Azure Repos and GitHub

Use Azure Repos and GitHub tools like Codespaces for development.

Objectives:

- Describe Azure Repos and GitHub.
- Migrate from Team Foundation Version Control to Git.
- Work with GitHub Codespaces.

### The Value of Azure Repos

- Free Git Repos, pull requests, and code search.
- Unlimited private repo hosting.
- Support for Team Foundation Version Control (TFVC).
- Support for any Git-compliant repository.
- Web Hooks and API integration with the Marketplace or build your own with REST APIs.
- Semantic code search.
- Threaded discussions and CI for each code change supports collaboration.
- CI-CD capability with triggers for build, test, and deployment.
- Pull Requests can be gated using policies including required code sign-off, etc.
- Use existing Git and TFVC repos with Azure Repos.

### Review What Is GitHub

The "Largest OSS community in the world" is GitHub, owned by Microsoft.

- Development platform.
- Git Repository hosting service.
- CLI and WebApp interfaces.
- Wikis, Issue Tracker, Project Manager tool, and more.
- Free for OSS project use.

Features Overview:

- Automate workflows for build, test, deploy, and other CI-CD.
- Automation in same same pane as development/IDE.
- Multi-lingual development and repo support.
- Packaging storage.
- Securing code and vulnerabilities in dependencies/packages, and from importing secrets, security tokens, and api keys.
- Semantic code analysis.
- Merge features such as code-review and sign-off, rebasing and squashing, discussion, and links to new or existing Issues.
- Issue tracking of work items, requests, and bug lifecycles.
- Store documentation alongside the code, including policy and licensing information, as well as developer, test, and deployment steps.
- Project management tools to stay on-course through tasks tracking and referential links between Issues, PRs, and code.
- Team organization through groups like owners and contributors, and manage rights to repository/project features and configuration items.

### Migrate from TFVC to Git

During a migration is a good time to "house clean" through restructuring a repo. It is usually fine to ignore history and only maintain the existing state and where it goes _next_.

1. Create empty Git repo(s).
2. Get the latest from TFS VC.
3. Copy and reorg the code into one or more empty Git repos.
4. Commit and push to the new remote GitHub repo.

:tada:

_Note_: I've completed such a task before using PowerShell to migrate from TFVC to GitLab repos, but it was for archived projects.

Single-Branch Import:

- Azure DevOps enables this feature.
- Only allows importing _one_ branch though.
- Rest of process is automated.
- This _does_ store up to 180 days of historical commits.

Git-FTS Migration/Importation:

- Is a `choco` package.
- Runs locally, requires PATHs setup, and .NET Framework 4.5.2 version of Team Explorer or Visual Studio (depending on Azure DevOps version that is the target).
- Allows multi-branch importation.
- Preserves relationships between branch histories.
- Can be a slow process for repos with long histories.
- Dry-run option allows viewing estimated execution to find problems early, and fix them before actually executing.
- _Subversion_ users: Use `GIT-SVN` to perform this migration work.

[GIT-TFS clone command readme](https://github.com/git-tfs/git-tfs/blob/master/doc/commands/clone.md).

### GitHub Codespaces Review

Aims to solve these problems:

- Old hardware and software systems that are not refreshed.
- Moving between physical systems requires configuration-time, which is counter-productive to the project.
- Lack of control of IP across multiple dev machines.

CodeSpaces is:

- Cloud-based IDE.
- _Is_ VSCode, running in a cloud instance.
- Multi-platform supports Windows and macOS clients.
- One or more available per GitHub repository.
- Connect-able to VS Code on local machine!

## Choosing DevOps Tools: Azure and GitHub

Explore Azure DevOps and GitHub tools to help manage work items and licensing strategy.

Objectives:

- Design a tool integration strategy.
- Design a license management stategy.
- Design a strategy for end-to-end traceability from work items to working software.
- Design an authentication and access strategy.
- Design a strategy for integrating on-prem and cloud-based resoruces.

### Azure DevOps

Provides services:

- Azure Boards for agile planning, tracking, visualization, and reporting.
- Azure Pipelines: Automatit CI-CD actions integrated with Containers or Kubernetes.
- Azure Repos: Cloud-hosted private Git Repos.
- Azure Artifacts: Package maangement supporting Maven, Python, NuGet, npm (and more), providing both private and public sources.
- Azure Test Plans: Integrated planning and exploratory testing.

Is cross-platform:

- Is _not_ Windows only.
- Independent service adoption to fit your project needs.
- Cross-platform support includes Linux, macOS, and languages like node.js, Python, Java, PHP, and more.
- Is cloud-agnostic, supporting AWS, GCP, and Azure.

Both Cloud _and_ on-prem services are available with Azure DevOps!

### GitHub Is a SaaS

- Provide Git-based repos.
- DevOps tooling for dev and deployment.
- CodeSpaces: Cloud-hosted VS Code IDE for cross-platform development.
- Repos: Git-based.
- Actions: Automate workflows and incorporate Env Vars and Scripts.
- Packages: For rolling-out software packages for open source.
- Security: Detailed code scanning and code review features.

Both CLoud _and_ on-prem services are available with GitHub!

### DevOps Authorization and Access

Azure DevOps has:

- Enterprise grade auth.
- MSFT, GitHub, and MSFT Entra ID support.

Personal Access Tokens are used for:

- Git-based Repos.
- NuGet.
- Xcode.
- Secure login popups.

Personal Access Tokens can be created manually or set up using Git-related cred managers.

Security Groups:

- Default permissions assigned in default groups, simplifying start-up.
- App-access policies allow alternating auth methods or using 3rd party auth, as well as anonymous access.
- Conditional Access Policies secure resources using MSFT Entra ID.

Multifactor Auth:

- Part of Conditional Access Policies.
- Defined by Sec Grp membership, Location or Network ID, specific OS, or managed device.

### Migrate or Integrate Tools to DevOps

Third-party integrations are allows. As an example, Visual Studio Marketplace allows integration with Trello.

Migration takes planning and significant work:

- Managing highly configured tools requires mapping to the DevOps solutions but DevOps Mgmt Tools are also highly configurable.
- Solidify offers a tool to migrate Jira issues into Azure DevOps.
- Custom migration code can be written and leveraged for migration actions.

Other Apps include Aha, BugZilla, and ClearQuest.

Test Management Tools can also be migrated to Azure DevOps:

- Visual Studio Marketplace has Azure DevOps Test Feedback Extension for exploratory testing.
- Apache JMeter: OSS Java for load test and performance testing.
- Pester: PowerShell code test automation tool.
- SoapUI: Test SOAP and REST calls, WRRC.
- MSFT Test Manager: Can be migrated directly to Azure DevOps.

### DevOps License Migration

Understand where in the tool migration process your team(s) are:

- As existing tool usage declines, license costs will change.
- As new users and usage increases in Azure DevOps, license costs and management will change.
- Multiple teams running queued jobs might hinder team workflow velocity, so paying for Parallel Task processing might be a valuable license cost. How much time is spent _waiting_ for queue jobs, and what does that cost vs using Parallel?
- How many users are actually using the licensed feature?
- Are all users going to use all features/services?
- What individuals and teams need access to what features and services?
- If an advanced Package Managemetn strategy exists, more space for Artifacts might be necessary, potentially adding to licensing costs.

## Assess Your Development Process

Goals:

- Explain the purpose of VSMs.
- Use a VSM to understand where to improve release process.
- Compute activity ratio or overall efficiency for devops processes.

### Analyze DevOps Processes

Analyze the teams current processes:

- How does the product move from development to production?
- When is testing done in the process?
- What does 'done' mean?
- Are there manual processes that could be automated?
- How well do the team members engage and 'get along'?
- Existing Artifacts: Deployment packages, NuGet, container repositories, etc.
- Existing Test-Management Tools.
- Existing Work-Management Tools.
- Recommend migration and integration strategies.

### Value Stream Mapping VSM

VSM helps _analyze current processes_:

- Show where value is created.
- Show where value is NOT created (waste).
- Pinpoint areas that are zero or negative value to the project as a whole.

Notes on how VSM Helps:

- [ ] In areas where the end-user/customer/stakeholder does not see any value, work on reducing the time to completion, or eliminating those steps completely.
- [ ] If workers cannot access code repository, this blocks progress and will negatively impact value of the end product.
- [ ] Notifications between team members should be nearly instantaneous so value is not lost while waiting for a notification or response.
- [ ] Manual processes that take days will reduce value by slowing productivity. Find ways to automate these processes (like testing).
- [ ] Triage should be done quickly to assign debug/fix work right away.
- [ ] Pre-production, dev, test, and other builds and deployments should be happening regularly and be as automated as possible. Also, build time-to-completion should be known and analyzed to find areas where time-to-completion/deployment can be reduced.
- [ ] Migrating from current processes to improved processes might take a few Sprint cycles to update the VSM, re-evaluate efficiency, and made adjustments.

Process Time: Value-add productivity time like coding a feature and pushing it to production.
Total Lead Time: The total amount of value-add and non-value-add time from start to finish of a process such as a feature.
Activity Ratio: Process Time divided by Total Lead Time.

Consider _Activity Ratio_ to be an efficiency in producing direct value to the customer.

## What is Azure DevOps

A suite of services that spans the entire DevOps life cycle.

- Planning
- Production
- Testing and bugfix
- Reporting
- Deployment
- Monitoring
- Support

Azure DevOps integrates with many other tools (e.g. Jenkins).

Objectives:

- ID what separates elite performers from low performers.
- List what services Azure DevOps provides.
- Create an Azure DevOps organization.

### DevOps Is

People + Processes + Products that enable coninuous delivery of _value to customers_.

See [Abel Wang, Cloud Advocate, Microsoft](https://www.youtube.com/watch?v=tqBFyJffkiY&pp=ygUJYWJlbCB3YW5n)

DevOps _is not_:

- A quick fix.
- A methodology.
- Specific software.
- A title.

Agile Planning: Use a work backlog that everyone has access to, where work can be listed, prioritized, tracked, and reported on.

Continuous Integration (CI): Automate building and testing code. Example: Upon every commit to a branch, a build and test process runs and reports are generated based on results.

Continuous Delivery (CD): Test, configure, and deploy from build to QA or production environments.

Monitoring: Telemetry acquires information about application performance and usage patterns. Feedback from monitoring is injected into future development cycles.

### An Elite Performing Team

Elite performers have these features:

- Deploy more frequently. Monitoring, continuous testing, DB change management, and integrating security early will help with this.
- Reduce lead time from commit to deploy. Smaller batches lead to shorter lead times.
- Reduce change failure rate.
- Recover from incidents more rapidly. Metrics, and deploying more frequently will help.

_Note_: Outsourcing functions tends to be a sign of a low-performing team, whereas elite teams tend to manage all the functions.

### Azure DevOps Tools

Collaboration

- Azure Boards: Plan, track, and discuss work. Can be cross-team enabed.

Automated Build processes

- Azure Pipelines: Build, test, and deploy using CI/CD workflows with any language, platform, or cloud.

Testing

- Azure Test Plans: Manual and exploratory testing tools.

Version Control

- Azure Repos: Git-based repos in Azure.

Package Management

- Azure Artifacts: Create, Host, and Share packages.

## Azure Pipelines

Decide on a pipeline strategy and responsibilities by understanding Azure Pipelines and their components.

Objectives:

- Describe Azure Pipelines.
- Explain role of Azure Pipelines and its components.
- Decide Azure Pipelines automation responsibility.
- Undersatnd Azure Pipelines terminology.

The following are notes taken while working through an AZ-400 level training module.

### What Is Azure Pipelines

- Fully featured service.
- Create cross-platform CI and CD workflows.
- Works with Git-based source controls.
- Supports deployment to most major cloud services.

Key Concepts:

- Product delivery creates value.
- Continuous delivery (CD) accelerates product deployment and refresh cycles.
- Create repeatable, reliable processes for the software development and deployment cycle through to delivery.
- Pipelines are created in stages.
- Quality is checked at every stage from varying perspectives.
- Feedback on pipeline stage processes are bubbled-up to the team.
- Optimize delivery in advance, resulting in quantifiable value to business.
- Enables continuous monitoring.
- Pipelines becomes the focus of the 'continuous improvement loop'.
- Build automation, CI, test automation, and deployment automation.
- "Works with any language or platform".

### Build Automation and CI

- Build binaries, generating devlierables.
- Pass deliverables to following stages.
- Provide insight into dev lifecycle and product health in this stage.

### Test Automation

- Unit testing.
- Security testing.
- Performance testing.
- Compliance testing.
- Manual and automated testing functions are performed at this stage.

### Deployment Automation

- Agile development's Continuous Delivery means deployments must happen at every stage of SDLC.
- Deployments can be staged before rolling out to Production.
- Automation eases effort to deployment, maintains consistency in deployment steps, and speeds time-to-delivery.

### Platform Provisioning and Configuration Management

- Teams create, maintain, and tear down environments through automated or manual triggers.
- Tests and other processes are always carried out with every environment.
- Enables horizontal scalability.
- Enables sandboxing at any time.

### Pipeline Orchestration

- Pipeline stages are managed and monitored by groups within the Org.
- Orchestration provides top-level-view into Pipeline operations and SDLC process through deployment.

### More Azure Pipelines Details

- Cloud-based sevice.
- Automates build and test processes.
- Provides build and test result reports to users in the Org.
- Multi-language, multi-project-type compatible.
- Combines CI and CD through to prodcut shipment.

Languages include:

- Python
- Java
- Ruby
- C#
- Go

Git-based Repo Compatibility:

- GitHub
- GitLab
- Azure Repos
- Bitbucket
- Subversion

Application Types:

- Web Apps
- Desktop apps
- Full-stack systems
- Cloud services

Deployment Targets:

- Container registries.
- Virtual machines.
- Cloud targets: Azure, Google Cloud, AWS.

Package Formats:

- NuGet
- npm
- Maven
- "any other package managemetn repository of your choice"

### About CI-CD

Continuous Integration (CI):

- Increase code coverage.
- Build faster by splitting build and test runs.
- Blocks shipping broken software through pre-publication staging and testing processes.
- Continuous test running capabilities.

Continuous Delivery (CD):

- Deploy code to Production, automatically.
- Maintain 'latest code' deployments to environments.
- Code is tested via the CI process.

### Azure Pipelines Key Terms

Triggers activate Pipelines containing Stages that activate Agents that fire Jobs and dependent Jobs in Steps such as Scripts and Tasks like Publishing Artifacts, Deploying a WebApp to Azure, or invoking a REST API.

Agents:

- Installable software.
- Runs one Build or Deployment job at a time.
- Can be hosted by MSFT or self-hosted.
- Platforms include Windows, Ubuntu, and others.

Artifacts:

- Files or packages published by a Build.
- Available for Tasks like distribution or deployment.
- Examples include: Java packaged into a .jar, .NET App packages into a Zip or MSI, C++ or JavaScript Libraries, or an _image_ for a VM, Docker, or the Cloud.

Builds:

- A single execution component of a Pipeline.
- Collects logs associated with running Steps and Test Results.

Continuous Delivery:

- Code is built, tested, and deploy to one or more test and production stages.
- CI-produced artifacts are consumed by CD as part of the deployment process.
- Monitoring and Alerting are integrated to report on status of the CD processes.

Continuous Integration:

- Simplifies testing and building of code.
- Catches bugs early in the development process, before deployment.
- Automates test and build processes.
- Can be scheduled, or fired whenever code is pushed, or both.
- Produces Arifacts as its output.

Deployment Target:

- Virtual machine, Container, Web Apps, etc.
- Services used to host an application.
- Multiple targets can be selected from a Pipeline configuration.

Job:

- Is an execution boundary of a set of steps.
- Contains 1 or more Jobs.
- Most Jobs run on an Agent.
- Job Steps are run on the same Agent.

Pipeline:

- Defines CI and CD processes.
- Made up of Tasks.
- Defines test, build, and deployment steps at a fine level of detail.

Release:

- Describes _one execution_ of a Release Pipeline.
- An output of a Visual Designer tool.
- Compiled of deployments to multiple stages.

Stage:

- The primary division of work in a Pipeline.

Tasks:

- Building blocks of Pipelines.
- Can consist of Build and Test tasks.
- Release Pipelines would consist of various deployment tasks, each running a specific tasks within the pipeline.

Trigger:

- Tells the Pipeline when to run.
- Configurable to fire from operations like `push` to a repo, or completion of another build.

### Azure Pipelines Key Concepts

Azure Pipeline Options:

- Build and develop with a local IDE and use a Microsoft-hosted Agent. This requires requesting and paying for Pipeline Hours.
- Build and develop in GitHub Codespaces and use a Self-hosted Agent. Free-tier usage hours are included and charges may accrue after an initial period. Self-hosted agents must be maintained by the users/team and must be registered with Azure DevOps in order to be used by Pipelines.

Map manual build steps to automated Pipeline Tasks:

- Create an Access Token in the Azure DevOps Organization and enable: Agent Pools Read & Manage. This will be used when Codespaces registers its agent with the DevOps Organization.
- Set up GitHub Secrets with `ADO_ORG` and `ADO_PAT` to allow using the Azure DevOps Org Token (in the exercise, these were set up as Codespaces Secrets, which using Codespaces for a real production-targeted Pipeline carries some risks it will work for an exercise). Also, Pools can be identified other than the default.
- Consider how current build, test, and deploy scripts operate. Plan for how to duplicate these in a Codespaces or other environment leveraging Azure Pipelines (build machine OS, required tools, SDKs, and Packages).
- Create Pipelines using YAML files, directly in the repo.
- Tasks under `steps:` in the `azure-pipelines.yml` file should map each existing step to a Pipeline `task` to do the same work as is done in-house manually, or through other automation or scripts.
- Build-in EnvVars are used to define Pipeline parameters (see the list below).

Built-in Pipeline Variables:

- `$(Build.Definitionname)`: Name of the build Pipeline.
- `$(Build.BuildId)`: Numeric ID for a completed build.
- `$(Build.BuildNumber)`: The Name of the completed build. Default format is YYYYMMDD.n where n is a numeral like 1 that can be incremented. Format can be configured.

Publish Builds for others to use:

- When a Build Pipeline completes, artifacts are stored on a temporary build server (by default).
- It is possible to simply output Artifacts for QA or other groups to consume, rather than push to a deployment environment direcly from a Pipeline.
- Use `$(Build.ArtifactStagingDirectory)` and a folder name to direct build output files to a location that can be used by other Jobs within the Pipeline.
- The Pipeline Tasks output (when a Pipeline is selected and all Tasks complete) displays "Repository and version", "Time started and elapsed", "Related", and "Tests and coverage" headers. Under Related will be links to Published items (if any). Drill-down into the published artifacts directory structure to find teh output file(s).
- Use EnvVars to make Pipeline Tasks more readable and simpler to maintain and update.
- Variable placeholders are replaced with Values as the Pipeline runs.
- Store repeated information in EnvVars such as: Version numbers, file paths, etc.
- Limit the use of variables to just what makes the most sense and has the most positive impact. Adding lots of variables can make the YAML file more difficult to read.
- Adding users to the Project causes emails to be sent to those users when Pipeline Jobs complete.

Implement Templates for multiple configurations:

- Rather than maintaining multiple versions of YAML files, each containing very similar scripts (such as a Release version and a Debug-build version), use Templates.
- Define common build tasks once and reuse them multiple times.
- A build step will be added to call the template from the pipeline.
- Parameters can be passed-in to the template by the pipeline.
- Create a templates directory at the project root (or another location based on team's needs or best practices), and create a new YAML file.
- Parameters are passed-in to the YAML file's `parameters:` section.
- Variables are passed-in to the YAML file by using `${{ parameters.paramName }}` syntax.
- When running the Pipeline, the Jobs summary will include additional information for the templated Job definitions from the YAML file.

### How Pipelines Process YAML file commands

The example provided in the learning module was as follows:

```yml
task: DotNetCoreCLI@2
  displayName: 'Build the project'
  inputs:
    command: 'build'
    arguments: '--no-restore --configuration Release'
    projects: '**/*.csproj'
```

```cli
dotnet build MyProject.csproj --no-restore --configuration Release
```

## Resources

- [Azure DevOps Pipelines Reference Documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/)
- [Learn YAML in Y Minutes](https://learnxinyminutes.com/docs/yaml)
- [Azure Pipelines Tasks Reference](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference)
- [Azure DevOps Services](https://azure.microsoft.com/en-us/products/devops/)
- [MSFT DevOps Resource Center](https://learn.microsoft.com/en-us/devops/)

## Footer

Return to [ContEd Index](conted-index.html)

Return to [Root README](../README.html)
