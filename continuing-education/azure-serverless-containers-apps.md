# Serverless Intelligent Apps on Azure Container Apps

Series of MSFT Reactor presentations on Serverless, Intelligent Apps, and Azure Container Apps.

## Table of Contents

- [Introduction](#introduction)
- [Azure Container Apps (ACA)](#azure-container-apps-aca)
- [Azure Developer CLI - azd](#azure-developer-cli---azd)
- [Deploying ACA with Dapr using azd](#deploying-aca-with-dapr-using-azd)
- [Resources](#resources)
- [Footer](#footer)

## Introduction

Presenter: Jonah Andersson, Sr. Azure Consultant at Solidify.

- Founder/Leader of Azure User Group, Sweden
- Fullstack .NET focused developer.
- Lead Cloud DevOps Engineer Architect.
- Author of Learning Microsoft Azure (O'Reilly).
- And much more.

Azure Functions? Not anymore! Now use Azure Serverless:

- Solve Queuing (workflow) problems.
- Events need to be able to wait on each other.
- Large, complex apps can be challenging to keep a manageble, performant workflow.

Serverless + AI + Cloud Native :arrow_right: Intelligent Apps.

### Serverless Computing

Not really serverless, right?

- Is an application development and execution _model_.
- Empowers developers to build and run app code without provisioning or managing servers or backend infrastructure.
- There _are_ still servers, but they and their configuration are abstracted for simplification for dev, build, debug, and run.
- Other cloud resources are serverless: DBs, Storage, Containers, Microservices, and Cloud Native.

### Serverless on Azure

- Azure Functions: Event-driven, serverless computer.
- Azure Durable Functions: Extension of Azure Functions for stateful, event-driven workflows.
- Azure Serverless Databases: Azure SQL Serveless, Azure Cosmos DB Serverless, etc.
- Azure Logic Apps: UI User WOrkflows for apps, data, and devices on cloud and on-prem using pre-built Connectors.
- Azure Kubernetes (AKS), Azure Container Apps (ACA), etc.

### Cloud Native

Cloud Native Computing Foundation defines Cloud Native technologies as:

- Containers.
- Microservices.
- Declarative, cloud-based APIs.
- Enable loosely coupled cloud systems.
- Robust automation.
- High-impact, frequent changes with 'minimal toil'.

MSFT Pillars of Cloud Native:

- Cloud Infrastructure: Microsoft Azure PaaS.
- Modern Design: 12-factor application, well architected framework for Azure.
- Microsofvices: Follows 'process' principle of 12-factor application.
- Containers: Code, dependencies, and runtime are packages into a binary "container image" that has Disposability and Concurrency features.
- Backing Services: ANy service the app consumes over the network as part of its normal operation.

### The 12 Factors

Search for the Twelve-Factor App to learn about:

- Codebase
- Dependencies
- Config
- Backing services
- Building, release, run
- Processes
- Port binding
- Concurrency
- Disposability
- Dev/prod parity
- Logs
- Admin Processes

### Monolithic vs Cloud Native

Cloud-native separates Client Apps from Cloud-hosted Docker/Web Apps with backing Micro-Services via an API Gateway to provide features and capability.

Workflow is managed by Event Bus (publish/subscribe channel) behind the microservices so event-based messaging is enabled.

Client App Examples:

- Mobile App.
- Traditional Web App.
- SPA Web App.

### Ideal Use Cases

Migration and Modernization of legacy application to the cloud.

- Two causes: Forced to by problem or policy, or by implementing cloud-native feature solutions.
- Deployment Models: On-prem, IaaS, Containers and PaaS, etc.

Using IaaS enabled "lift and shift" migration method which could be quick, and enables full migration to cloud native as a whole.

## Azure Container Apps (ACA)

Serverless, container-based hosting service.

- Focuse on apps instead of infrastructure.
- Event-driven scale from zero to many.
- No-pay when not in use (zero scale).
- Fast, dynamic scaling to handle incoming requests.

Build Ideas:

- Microservices.
- Public API Endpoints.
- Web Apps.
- Event-driven Processing.
- Background Processing.

Auto-Scaling:

- Individual microsoervcices can scale indipendently.
- Scaling determined by number of concurrnt http requests.
- Number of messages in the Queue informs auto scaling feature.
- Level of CPU and memory load also drive scaling automation.

Benefits:

- Serverless, pay-per-use.
- Automatic scaling.
- Run containers from any registry (Docker etc) or Azure Container Registry (ACR).
- Unified Management: Azure CLI, Portal, etc.
- Microservices using Dapr.
- Itegration with servless like Azure Functions.
- Traffic splitting for blue-green deployments.
- Internal ingress and DNS-based services discovery.

ACA can be a Container App _Environment_:

- Container Apps work in concert to act as the primary service.
- Other serverless features like Costmos DB, Cache for Redis, Managed Identities, and Azure Service Bus.
- Azure App Insights, zure Monitor, and Log Analytics can be plugged-in to the Container App Environment.

Managing Complexity of Microservices:

- Dapr does this!
- Provides Building blocks and complonents to build microservices.
- Hosting can be done by Azure, AWS, Google Cloud, etc.
- Dapr: Provides APIs to simplify microsorvice connectivity.
- Dapr suports Pub/Sub messaging and Service Invocation models.
- Service discovery, message broker integration, encryption, observabilitym, Secrets, and Configuration are managed by Dapr Sidecar.
- Dapr Sidecar can be thought of as a daemon that sits between the Container App and the custo Component.
- Dapr Sidecar uses Service Bus to manage these communications.

## Azure Developer CLI - azd

Is an open-source, developer-centric tool.

- Azure CLI is the Administrative version of this.
- AZD is focused on Developer needs to build and deploy WebApps.

Building An App For Cloud:

- Planning.
- Proof of Concept.
- Team.
- Responsibilities.
- Tech Stack selection.
- Tools for the team: Dev, Test, CI, Deployment, Debug, etc.

Other considerations:

- Frontend platform and type.
- Backend platform and type.
- DevSecOps and CI-CD
- IaC: Infrastructure as Code selection.
- Cloud integration and service considerations.
- Testing and Automation.

AZD Features:

- Developer-centric cloud developent tool for Azure.
- Templates to speed development and simplify workflow.
- Open-source, ployglot.
- Good for Proof-of-Concept projects.

Workflow:

1. Select azd template.
2. `azd init --template [template name]`
3. Code and configure infra, params, azure.yml.
4. `azd up`
5. Iterate code changes.
6. `azd deploy`

Cycle through 5 and 6 through the lifecycle of App development.

`azd provision`: Optionally update Azure resources by modifying the template Infrastructure as Code (IaC).

`azd monitor`: Opens Azure AppInsights Metrics locally.

Locally develop:

- PowerShell, VSCode plugin.
- GitHub Codespaces.
- DevContainers.

## Deploying ACA with Dapr using azd

This was a live demo and the following are random thoughts while watching the demo:

- Using a 'typical azd template' project.
- Is a local project that Jonah will push to cloud using azd.
- Uses pub-sub via Azure Service Bus.
- Can be configured to use DevContainers, or build in GitHub, using dockerfiles and yaml.
- azd Templates enabled quick spin-up of Terraform or OpenAI services behind your ACA project.
- dapr has a Terminal command-line that enables running the Project with named resources and tcp port.
- In the Q&A it was noted that ACA is probably simpler to setup and get running that AKS (Azure Kubernetes Service).
- `azd up`: Does package checkout, build, and creates Containers Endpoint, and logs these activities in the Terminal.

## Resources

About [Azure Container Apps and Dapr](https://aka.ms/aca-dapr).

More about [Azure Developer CLI 'azd'](https://aka.ms/awesome-azd).

Jonah's [Blog article on azd](https://bit.ly/azuredevelopercli-azd).

Learning path for [Azure Container Apps (ACA)](https://aka.ms/COntainerAppsDocs).

Learning path for [Azure Developer Cli (azd)](https://aka.ms/azd).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
