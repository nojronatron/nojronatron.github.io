# MS Reactor Graph API with DotNET

GraphAPI and DotNet help to automate and integrate:

- Automate: Do stuff hands off, work without my additional input.
- Integrate: Two or more applications that have little/nothing to do with each other working as a single app.

## Introduction

Scott Hanselman

Yina Arenas @yina_arenas

## Notes

MS Graph is a:

- Cloud-based REST API.
- Data structure for MS-365 data.
- Pattern of productivity, ID, and security in an Org, described by the Data stored in it.
- Set of tools that enable building apps to integrate with MS 365.

Why MS Graph?

- Organizations have people and business interactions around the world.
- Ability to see Calendar, Contacts, etc.
- Connects all the information together.
- Simple integration with MSTeams.
- No longer have to use App-specific APIs (e.g. Outlook).

Does not run on client.

Graph Allows:

- Office application automation: OneDrive, PowerPoint, Outlook, etc.
- Integrate with Azure Functions.

Graph API:

- Graph Explorer: Like Swagger for MS Graph API.
- Slash 'me': The standard, fluid (semantic) endpoint for common operations about you and your data.
- Returns: standard JSON.

Requires:

- Azure ActiveDirectory account for Enterprise customers.
- Customers can use Hotmail, Live, MSN (any end-user type) account.
- An Azure Subscription: Necessary to register your data with MS Graph.

*Note about Azure Tenant*: Describes an organization that has an account with Office365 or Azure, etc.

Code Snippets: Generates code in client languages:

- CSharp
- JS
- Java
- Go
- PowerShell

*Note*: PHP and Python are also available (but not necessarily directly from the CodeSnippets tab).

## Code Steps

1. Create scopes (an Array of settings you want to get).
1. Obtain from MSGraph or Browser-credential storage and create the Credential object.
1. Make a Graph service and include the credential and the scopes.
1. Check if Graph Service has the event already.
1. Create a Graph Todo aka Task.
1. Create the Graph Event and ensure the correct timezone and offset are expressed.

## Get Started With the Graph.NET SDK

### Hosts

Ayca Bas

Waldek Mastykarz

Rabeb Othmani - MS Graph PM :arrow-right: /in/othmanirabeb, @Rabeb_Othmani

Maisa Rissi - MS Graph PM :arrow-right: /in/maisarissi, @maisarissi_msft

### Agenda

- What is MS Graph
- What information is available from MS Graph
- How to call MS Graph APIs
- How to use MS Graph in .NET apps

### Get Involved

1. Register at https://aka.ms/hack-together/register
2. Clone the template code
3. Code! Use MS Graph DotNET SDK
4. Submission: github.com/microsoft/hack-together and share your repo in an Issue
5. Schedule: 1-March through EOD 15-March

Maximum team size: 4

### Criteria

1. Does the app work?
2. Does the app use the MS Graph .NET SDK?
3. How creative, innovative, and polished is the app?

Meeting criteria 1 & 2 earns a digital badge award.

Meeting all 3 criteria puts the app in evaluation process for top prizes.

### Dive Into Graph

Use Graph Explorer:

- Free sample data available at [ge](https://developer.microsoft.com/en-us/graph/graph-explorer)
- Uses a testing tenant with sample data for dev and test.
- Only allowed GET operations.
- Create a Tenant by registering in Azure Portal first.
- Use your Tenant to interact with REST to see your data.

### Installing and using the SDK

There are different SDKs, tied to each language.

#### Microsoft Graph Java SDK

For Java:

- MS Graph Java SDK
- microsoft-graph: Models and request builders to access v1.0 endpoints with fluent API.
- microsoft-graph-beta: Models and request builders for accessing beta endpoints with fluent API.
- microsoft-graph-core: Core library for making calls to MS Graph.
- microsoft-graph-auth: Provides authentication scenario-based wrapper of MSAL (MS Auth Library).

Use Gradle to install the SDK via dependency object:

```java
dependency {
  implementation 'com.microsoft.graph:microsoft-graph:5.+'
  implementation 'com.azure:azure-identity:1.+'
}
```

Create an MS Graph client:

- Instantiate ClientSecretCredential, chaining clientId, clientSecret, tenantId, and build
- Instantiate TokenCredentialAuthProvider and provide Scopes and instantiated clientSecretCredential
- Instantiate GraphServiceClient, chaining builder, authenticationProvider, and buildClient

Client Middleware:

- Order of insertion is important.
- Default set allowed comms with SDK Endpoints.
- Add a logger to provide insights.
- Add a test handler middleware to simulate specific scenarios.
- Once a Client is instantiated, the middleware is inserted using chained function calls.

Client Proxy:

- Necessary if behind a proxy server.
- If proxy requires authentication, the middleware can be configured for that too.

Authentication Provider:

- Add the appropriate Identity library (Java: azure-identity).
- Client credentials provider allows non-interactive authentication e.g. Application ID.
- On-behalf-of Provider.
- Device code provider: Authenticate by way of another device.
- Integrated Windows provider.
- Interactive provider: Call Graph API in the name of the user.
- Username-password Provider: Use only if other OAuth flows are not possible.

Scopes:

- Allow access based on rules.
- Scope constrains access to data or endpoints that might not apply to a scenario.
- Certain scopes are defined to get to the proper endpoints and REST operations.

#### Microsoft Graph DotNET SDK

(more to come)...

## Resources

MS Graph [SDK Overview](https://learn.microsoft.com/en-us/graph/sdks/sdks-overview)
SDK Install for [Java](https://learn.microsoft.com/en-us/graph/sdks/sdk-installation#install-the-microsoft-graph-java-sdk)
MS Graph [Best Practices](https://learn.microsoft.com/en-us/graph/best-practices-concept)

## Footer

Return to [ContEd Index](./conted-index.html)

REturn to [Root README](../README.html)
