# The MSFT Identity Platform

Microsoft Identity Platform helps manage identities and aspects of AuthN and AuthZ. Write-ups on this page will collect thoughts, notes from seminars and online sesions, as well as research discoveries revolving around MSFT ID Platform.

## Azure Friday Episode 25-June-2021

Host: Scott Hanselman

Guest and Presenter: Christos Matskas '@christosmatskas'

### Overview

Why roll your own identity architecture? It's not really recommended, but what service can you trust and what features will be helpful to your project (and organization)?

Christos says it is *not your job to write your own ID layer*.

Compromises continue to happen to organizations that take the complex route of 'rolling their own ID infrastructure'.

Identity might not be sexy, but it is a required service in today's tech-heavy world, and must be managed.

MSFT ID Platform is built on top of Open-ID technologies.

MSFT ID has hudreds of developers building, improving, and managing the ID Platform *so you do not have to*.

Why would you want to store your user's passwords? Breaches regularly make passwords available to hackers.

Azure Active Directory:

- Scalable.
- World's largest cloud ID service.
- Includes access management.
- Is behind the scenes when leveraging MSFT ID Platform.

MSFT ID OOB Capabilities:

- MFA: Just 'flick a switch' and it is on!
- Fencing types are available for free, without coding custom fencings.

### MS ID Platform for Developers

- Register your App with MSFT ID Platform. This allows the App to leverage the service to enable AuthN and AuthZ.
- MSFT ID Library: Implement this in your code using MSFT Auth Libraries and OIDC Certified Endpoints.
- Web APIs: MSFT Graph, Azure, and your own APIs.
- Supported Identities: Work and School accounts, Personal accounts (games, mobile/web app, commercial services), External Entities (leveraging any OpenID Provider).
- Backwards compatible with SAML.

*Note*: You can bring your own library, not limited to MSFT OIDC Libraries.

Includes support for Android and iOS, as well as Windows.

### ID Within the MS Ecosystem

Additional benefits here when using:

- GitHub
- VSCode / Visual Studio
- MSFT 365 Platform
- Azure Services

Easier to implement and integrate security into your application.

### Demo

1. Create new DotNet application.
1. Use flag `--auth name` to download and install libraries for Azure AD integration.
1. CD into project and open VSCode / Visual Studio. Depending on the template, parts of the code will be implemented already.
1. Open Startup.cs and configure `ConfigureServices()` to add `MicrosoftIdentityWebAppAuthentication(Configuration)` as an IServiceCollection services member.
1. Open Azure AD and create a new Application Registration.
1. Configure the Platform (ASP.Net => Web, etc), define Redirect URIs, Logout URL, etc.
1. Azure AD App Registration will provide an Application ID. Add that to your application in `appsettings.json/AzureAd`.
1. Save changes in Azure AD App Registration settings, and the DotNET Application and run it.

*Note*: This is a lot like Auth0 setup and configuration. MSFT I Platform will also do the redirect login screen.

Summary:

1. Create App if not already exists.
1. Register App in Azure AD.
1. Add 1 line of code to the App.
1. Edit/handle 4 configuration items between the App and the Azure AD registration.

DONE!

## Resources

AzureFriday [An Intro to Microsoft Identity Platform](https://learn.microsoft.com/en-us/shows/azure-friday/an-introduction-to-the-microsoft-identity-platform).

[MS ID Platform Docs](https://learn.microsoft.com/en-us/azure/active-directory/develop/).

[Code samples](https://learn.microsoft.com/en-us/azure/active-directory/develop/sample-v2-code).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
