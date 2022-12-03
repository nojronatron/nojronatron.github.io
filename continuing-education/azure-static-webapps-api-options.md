# Azure Friday: API Options Azure Static WebApps

## Host and Guest Info

Host: Scott Hanselman

Guest: Annina Keller, MSFT Software Engineer, Azure Static WebApps team

## Summary Notes

Host static webapps with API endpoints and authentication!

URL includes '*.azurestaticapps.net'.

Managed Functions (deploying code from repository) are supported.

Node.js API as a WebApp or Container App?

- Bring in a functino app.
- Bring in back end services.
- Linking back-end services are secured.
- CORS is handled.
- Authentication from the front-end can be used on back-end via HTML Headers.

Host your own backedn service in a container app, and then connect the Static WebApp to it.

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

When logged-on to the Static WebApp, add '.auth/me' to the URL and Azure will return the clientPrincipal JSON including:

- ID Provided e.g. AAD
- UserID: {guid}
- User Details: Email address.
- User Roles: Anonymous, Authenticated, etc.

Supports multiple pre-configured OAuth providers like Google, Twitter.

Also supports bringing your own OAuth provider.

## Footer

Return to conted index

Return to Root README
