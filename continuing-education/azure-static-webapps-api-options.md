# Azure Friday: API Options Azure Static WebApps

## Table of Contents

- [Host and Guest Info](#host-and-guest-info)
- [Summary Notes](#summary-notes)
- [Demo](#demo)
- [Another Demo](#another-demo)
- [Kewl Stuff](#kewl-stuff)
- [Additional Learnings](#additional-learnings)
- [Static WebApp Provisioning Service](#static-webapp-provisioning-service)
- [Static WebApp Fallback Route](#static-webapp-fallback-route)
- [Static WebApp CORS Handling](#static-webapp-cors-handling)
- [Azure Static WebApps Key Features](#azure-static-webapps-key-features)
- [Azure Static WebApps Key Practical Concepts](#azure-static-webapps-key-practical-concepts)
- [Resources](#resources)
- [Footer](#footer)

## Host and Guest Info

Host: Scott Hanselman

Guest: Annina Keller, MSFT Software Engineer, Azure Static WebApps team

## Summary Notes

Host static webapps with API endpoints and authentication!

URL includes '*.azurestaticapps.net'.

Managed Functions (deploying code from repository) are supported.

Node.js API as a WebApp or Container App?

- Bring in a function app.
- Bring in back end services.
- Linking back-end services are secured.
- CORS is handled.
- Authentication from the front-end can be used on back-end via HTML Headers.

Host your own backend service in a container app, and then connect the Static WebApp to it.

## Demo

API's tab of Static WebApps enables defining the backend resource name in a subscription:

- Magic is in the PATH with '/api' prefix, and the entire path needs to match the endpoint's definition path.
- API Context = endpoint path e.g. '/api/path'.
- Any request matching the api prefix will get rerouted to the backend.
- This can be applied to enable authentication and authorization like preconfigured auth provider(s).

Authentication:

- Code: API extracts client principal details from headers.
- The redirect to the back-end via Azure allows extracting the detail and do identification, including UserID and Provider.

Authn and Authz is OOB capability for this feature.

Any request from the static webapp to the container app will contain the header that the backend app will use to handle authN and authZ.

## Another Demo

App combines 'this' with a new feature from API Management.

Setup:

- Use GitHub issues to collect feedback and logs etc.
- Only GitHub account holders are allowed to use the GH Issues service for yoru Repo.
- Login on front-end app already tied-in to backend API Azure Endpoint.
- But GitHub doesn't know who this ID is!
- An OAuth intermediary must handle tokens to be an 'identity proxy'.

API Management handles ID Proxying:

- Configure an OAuth App e.g. GitHub.
- Define a certain scope for the OAuth App to apply to.
- IPAM service is connected in the back-end to manage token proxying.
- Some code in the front-end will send a post to the correct api endpoint and can then set the body, title, and other properties for posting to the target GH Issues URL.

## Kewl Stuff

### Auth Me

When logged-on to the Static WebApp, add '.auth/me' to the URL and Azure will return the clientPrincipal JSON including:

- ID Provided e.g. AAD
- UserID: {guid}
- User Details: Email address.
- User Roles: Anonymous, Authenticated, etc.

Supports multiple pre-configured OAuth providers like Google, Twitter.

Also supports bringing your own OAuth provider.

## Additional Learnings

The following headings are from additional exploration beyond the presentation introduced above.

## Static WebApp Provisioning Service

From MSLeaern documentation:

>"Azure Static Web Apps takes care of provisioning all the necessary Azure resources for you."

> "A key feature of Azure Static Web Apps is that it sets up a GitHub Actions workflow to build and publish your application."

> "The workflow is triggered immediately and takes care of building and publishing your app."

> "The workflow is also triggered every time you make a change to the watched branch in your repository."

Two Major Steps:

1. Provision Azure Resources.
2. Set up GitHub Actions workflows for build and deploy.

> Sign in to GitHub to connect the Azure Static WebApp to the source GitHub Repo.

It will be necessary to share the Startup Project directory (at least) in order for Azure Static WebApps to set up the GH Actions properly.

Build artifacts should be published to 'wwwroot' folder.

_Note_: If API is an Azure Functions project, Azure Static WebApps will host the Azure Functions (automatically?).

_Note2_: If the API project is not ready for publishing, it is not required to successfully deploy the Static WebApp. When it is added, the publish operation will include the API project at that time, provisioning the needed Azure Resources (automatically?).

## Static WebApp Fallback Route

Also known as a rewerite rule.

Use a fallback route to ensure that a failed page load (no API contacted, other network error, etc) brings up a page to the web user.

Name the file `staticwebapp.config.json` and store it anywhere in the app's source code folder.

```json
{
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/_framework/*", "/css/*"]
  }
}
```

## Static WebApp CORS Handling

Static WebApp with Azure Functions API project handles CORS issues for you, so no additional CORS handling is necessary.

- Azure Static WebApps auto-deploys a Reverse Proxy to handle CORS requests for you.
- Configure `launchSettings.json` to configure the CORS Setting in the API server.
- `launchSettings.json` configures the API Server so that requests usingn Visual Studio are not blocked by default.
- Generally speaking, `launchSettings.json` should be **git ignored** and _not_ pushed to a Git repo.

```json
{
  "profiles": {
    "Api": {
      "commandName": "Project",
      "commandLineArgs": "start --cors *"
    }
  }
}
```

## Azure Static WebApps Key Features

- WebApps will be globally distributed, lowering load latency to web site visitors.
- Get an automated build pipeline for CI/CD.
- WebApps are automatically secured with a (free) SSL Certificate.
- Simplify reverse-proxy implementation for dev/test usage using Visual Studio.

## Azure Static WebApps Key Practical Concepts

- Publish updates to Azure Static WebApps by pushing commits to the watched branch, or creating a PR to the watched branch.
- View build and redeploy progress by opening the Actions menu at the GitHub repo.
- Configure Static WebApp with a fallback route by editing `staticwebapp.config.json` that points to `index.html`.
- Configure Azure Static WebApps with a new API path by editing the build and deploy YAML in `.github/workflows`.

## Resources

- Video Series: [Deploy Azure Static WebApps to the Cloud](https://learn.microsoft.com/en-us/shows/deploy-websites-to-the-cloud-with-azure-static-web-apps/)
- MS Learn Module [Publish an Angular, React, Svelte, or Vue JavaScript app with Azure Static Web Apps](https://learn.microsoft.com/en-us/training/modules/publish-app-service-static-web-app-api/)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
