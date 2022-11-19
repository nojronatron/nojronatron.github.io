# Azure Friday Episode: Introducing the Azure Developer CLI (azd)

## Presenters

Host: Scott Hanselman

Guest: Savannah Ostrowski

Originally aired 11-Oct-22

## What Is It

New CLI for Application Developers.

AZ vs AZD??

- AZ: Front end to Azure API.
- AZD: Map Azure management commands to abstracted commands, simplifying configuration and implementations in Azure.

Administrivia: High cognitive load.

## Demo Notes

Is what I'm doing secure? Are the correct infrastructure and services being deployed for my application development?

Bsst Practices + Infra As Code + Tools => App Running in Azure with CI-Cd and Monitoring.

Templates:

- Many already exist.
- Guidance available to help build your own.
- "Use This Template" -> Allows templating a Repository to your own GitHub repo, rather than just Clone it.

Pull program from GitHub: `azd init`. Prompted to then:

- Select a template, including 'empty'.
- A new environment name: An Azure Resource Group, specific to AZD.
- Region: An Azure Region.
- Subscription: Point to an existing subscription.

WSL is supported!

Directory `.azure`: Stores the environment created with azd init aka 'dot env file'.

Init codebase, provision and deploy in one command: `azd up`

All of the items that are provisioned upon deployment are displayed on the CLI output.

By default, AZD builds a shared Dashboard with monitoring and logging tools!

CosmoDB can also be created, via a Bicep file.

Get AZD:

- Preview Release Blog Post published in July 2022.
- CLI can be used within VS Code.
- Preview Feature also available in Visual Studio.

## Takeaways

This is very similar to AWS Amplify CLI.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [ROOT Readme](../README.html)
