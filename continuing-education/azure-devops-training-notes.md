# Azure Dev-Ops Training Notes

## Table of Contents

- [Assess Your Development Process](#assess-your-development-process)
- [What is Azure DevOps](#what-is-azure-devops)
- [Resources](#resources)
- [Footer](#footer)

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

## Resources

[Azure DevOps Services](https://azure.microsoft.com/en-us/products/devops/)

[MSFT DevOps Resource Center](https://learn.microsoft.com/en-us/devops/)

## Footer

Return to [ContEd Index](conted-index.html)

Return to [Root README](../README.html)
