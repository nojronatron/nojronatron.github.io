# Deploy React Site To Azure Web App

Azure Web Services includes support for 'static' HTML + CSS sites.

This appears to support JS, so I will assume that React.js is also supported - if not then I'll use a Node.js checklist instead.

## Setup

1. Clone the target repository to local.
1. Execute 'npm install' to ensure it is up-to-date. Fix any errors.
1. Open in VSCode.
1. Open Azure Extension.
1. Expand your Subscription.
1. Create a new Resource Group w/ name and Geo Location (for example: US West 3).
1. RClick App Services and select New Web App.
1. Give is a globally unique name; Node.js version (16); Pricing Tier.
1. Do not deploy it yet.

## Deploy

1. RClick the new App Service (WebApp) created above.
1. Select Deployment Source and then select LocalGit (this could be RemoteGit in future).
1. Open Application Settings and select 'SCM_DO_BUILD_DURING_DEPLOYMENT' and set to 'true'.
1. Update 'WEBSITE_HTTPLOGGING_RETENTION_DAYS' to whatver makes sense (7 days is default).
1. RClick the new App Service (WebApp) and click 'Deploy to WebApp' and select the correct local folder.

Note: If prompted to 'always deploy to this App Service' response Yes for simplicity.

## Test Deployment

Once deployement succeeds:

- Stream Logs => Displays running log to local 'Output' view, directly from connected to webapp container.
- Browse Website => Opens deployed webapp in your default browser.

## Next Steps

- Deploy an API Server.
- Deploy a Database or use MongoDB Atlas.
- Integrate Authentication and Authorization.

## References

Take a peek at:

[ms-identity-javascript-react-tutorial repository](https://github.com/Azure-Samples/ms-identity-javascript-react-tutorial)
[todo-nodejs-mongo](https://github.com/Azure-Samples/todo-nodejs-mongo)
[nodejs-docs-hello-world](https://github.com/Azure-Samples/nodejs-docs-hello-world)
For the Azure Storage, Cosmos DB portions (maybe AzAD depending on OAuth etc)[msdocs-javascript-nodejs-server](https://github.com/Azure-Samples/msdocs-javascript-nodejs-server)
[app-service-web-html-get-started](https://github.com/Azure-Samples/app-service-web-html-get-started)

## Footer

Return to [Root README](../README.html)
