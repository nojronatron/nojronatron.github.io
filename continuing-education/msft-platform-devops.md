# Modern DevOps on MSFT Platform Seminar

Presented by MSFT Reactor.

Hosted by MSFT MVP Magnus Timner, VP, DevOps Consultant, Solidify

Guest Mathias Olausson, CTO of Solidify

SDLC
Planning and Agile
CI and D
GitHub Actions
Automated Azure Dpeloyments
Test-Build-Release
Monitor Deployed Apps

## SDLC and DevOps

### What is SDLC

Software Development Lifecycle is a cycle, repeating these steps:

1. Plan
1. Analyze
1. Design
1. Implement
1. Test and Integrate
1. Maintain

### What is DevOps

1. Plan and Track
1. Develop
1. Build and Test
1. Deploy
1. Operate
1. Monitor and Learn

## GitHub SDLC and DevOps

Supports Hybrid SDLC and DevOps cycles:

Plan, Code, Build, Test, Release, Deploy, Operate, and MOnitor.

Using GitHub with SDLC:

- Plan: Issues and Product Boards
- Code: VSCode on online GitHub environments
- Build: Compile, build, and store artifacts
- Test: Unit tests, linters, and package consumption
- Release: Publish realease, upload artifacts
- Deploy: App to a platform
- Operate and Monitor: Use Azure (mostly out-of-scope for this presentation)

MSFT owns GitHub.

Azure DevOps (was VSTFS/VSS) works with Azure Repos and GitHub.

### Plan The Work With Requirements

Overview:

- Issues to plan requirements
- Actional tasks are small portions of Issues
- Plan work with boards, tables, and roadmaps
- Move vonversations from Issues to Markdown, Issues, etc.

### GitHub Work Items aka Issues

Markdown, Links, Labels, @Mentions, and Task Lists:

- Tasklist: '[tasklist]' following 3 ticks
- Mentions: `@username` notifies a user when mentioned.
- Diagrams: Instead of inserting pictures, use [Mermaid Syntax](mermaid.js.org) to design the diagram in markup!
- Sub-Activities: Step-by-step bullet or checklist items (in Beta). Can also convert checklist items to an Issue.
- Templates: Standardize Issue format and layout, pre-filled fields, pre-set labels.

Issues can be added from multiple Projects or various Repos in the same Project.

### Pull Requests

Check out 'dependabot'.

### Project Plan

RoadMap Tab: Sort and Filter Issues to get an overview of Issues, PRs, etc.

Burnup Diagrams: Shows charts based on tasks by assignee, etc. Columns and various other layouts available.

### Automation

Workflows determines what state changes in Issues or Pull Requests trigger setting values e.g. Status 'ToDo'.

## CICD

CI: Improve software dev quality and speed. GitHub Actions assists with building apps in the cloud.

CD: Ensures code and infrastrcuture are always ready for production.

Continuous Deployment with CI-CD: Think of this as a conveyor belt of building and puting code into production.

Cycles:

1. Local development: Local dev environment; code policies.
1. CI - Inner loop of building and testing: Automated build, code scanning, packaging.
1. CD - Outer Loop of validation and releasing: Environments; Approvals and governance; deployemnt.

### GitHub Actions

Actions Hub: Contains created Workflows and allows creating new Workflows.

Workflows: YML files :arrow_right: automates manual tasks.

- Triggered by specified Actions (push, pull, etc).
- Specify build job run location using GitHub Enterprise build runners, or custom ones, as well as specifying the build environment (Windows, Linux, etc).
- Run Commands: Execute specific commands with optional arguments.
- YAML script is committed to your repo along with the project.

New Workflows allow using a Starter Template targeting one of many possible technolgies: .NET, Node.js, etc. Generate a started YML script.

YAML Files can be edited online in GitHub, and if necessary, a PR created with the changes prior to merging with a specified or protected branch.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
