# MS Reactor Graph API with DotNET

GraphAPI and DotNet help to automate and integrate:

- Automate: Do stuff hands off, work without my additional input.
- Integrate: Two or more applications that have little/nothing to do with each other working as a single app.

## Introduction

Scott Hanselman

Yina Arenas @yina_arenas

## Notes

MS Graph is Cloud-based REST API.

Does not run on client.

allows office application automation: OneDrive, PowerPoint, Outlook, etc.

Can integrate with Azure Functions.

Graph Explorer: API Playground - like 

Graph API:

- Slash 'me': The standard, fluid (semantic) endpoint for common operations about you and your data.
- Returns: standard JSON.

Requires:

- Azure ActiveDirectory account for Enterprise customers.
- Customers can use Hotmail, Live, MSN (any end-user type) account.
- An Azure Subscription: Necessary to register your data with MS Graph.

Code Snippets: Generates code in client languages:

- CSharp
- JS
- Java
- Go
- PowerShell

*Note*: PHP and Python are also available (but not necessarily directly from the CodeSnippets tab).

Azure Tenant: Describes an organization that has an account with Office365 or Azure, etc.

## Code Steps

1. Create scopes (an Array of settings you want to get).
1. Obtain from MSGraph or Browser-credential storage and create the Credential object.
1. Make a Graph service and include the credential and the scopes.
1. Check if Graph Service has the event already.
1. Create a Graph Todo aka Task.
1. Create the Graph Event and ensure the correct timezone and offset are expressed.

## Footer

Return to [ContEd Index](./conted-index.html)

REturn to [Root README](../README.html)
