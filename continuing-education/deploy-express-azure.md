# Deploy NodeJS To Azure App Service

## Objectives

- ID correct options for deploying Node.js App to Azure
- Deploy Express.js webapp to Azure
- Understand how to access logs and debug Azure App Service
- Find additional information.
- Utilize VS Code Extension 'Azure App Service'

## Azure Services

Subscriptions contain Resource Groups that contain Resources including instances of services e.g. Azure App Service.

Resource Group:

- Logical unit.
- Name it so finding, managing related resources is easy.
- Geo-location definition e.g. USWest.
- Tags: Simplify finding and categorizing Resource Groups and other resources (up to 50 tags allowed).

## Tools

To Create A Resource Group, use:

- VS Code Extension: Developer tasks integrate Azure actions within same UI, IDE.
- Azure Portal: WebUI.
- Azure CLI: Automation tasks.
- PowerShell: Automation tasks.
- Azure SDKs for Management: Automation with lots of customization

Use the Azure tools to:

- Login to Azure using existing creds.
- Select the proper Subscription.
- Select the proper Tenent to create Resources and Resource Group in.

*Note*: From my workstation, the Azure Extension was very slow.

## App Service Plan

Express.js is a server-side app, so the following service plans would be appropriate:

- Azure App Service: Windows or Linux or container; Full control to configure and control the App.
- Azure Container, Kubernetes, Container Apps, and Virtual Machines: More work to set up but entire system is provided in hosting environment.

App Service Plan defines the compute resources for the webapp to run on (an abstracted 'server farm').

- OS.
- Region.
- Number of instances.
- Size of instances.
- Pricing tier (Free, Shared, Basic, etc).

One or more apps can be hosted within the same App Service Plan.

Resource-intensive apps should be moved into their own App Service Plan to avoid negative impacts on other apps in the same plan.

## App Settings at Creation

Required Configuration Items:

- Name
- Resource Group
- Runtime Stack (Node.js, etc)
- OS
- Location
- Pricing Tier
- Azure Application Insights: Captures app metrics and logs to the cloud (rather than in the App Container).

*Note*: It looks like Application Insights must be enabled at the Azure Portal.

## Post-Creation Settings

- CORS
- HTTP/HTTPS and TLS
- Port Forwarding
- Custom Domain
- Certificates
- Authentication and Authorization

## Env Settings

`const port = process.env.PORT || 8080;`
`WEBSITES_PORT 3000`
`SCM_DO_BUILD_DURING_DEPLOYMENT True`

## Public WebApp URL

'https://your-resource-name.azurewebsites.net/'

## Default Web App

Change 'hostingstart.html' static file to branding or contact information, as a splash page until the site is fully deployed.

## Authentication

Wide-open at initial deployment.

Post-deployment, configure to use social sign-ins, an AD authentication service, or a custom authentication platform.

Some programmatic changes within the App might be necessary to enable authentication and authorization.

## App Service Node Components

Application Settings: Env Vars

Databases: Only populated if DB is created at same time as this App Service.

Deployments: List

Files: This is where hostingstart.html is stored. Other files will be stored here for this resource to use.

Logs: Running App Log Files.

WebJobs: Not available for Linux Apps.

Deployment Slots: Slots to expanding deployments to handle higher loads.

## NPM Packages

Recommendation is to allow Azure to install all NPM Packages:

`SCM_DO_BUILD_DURING_DEPLOYMENT=true`

Optional: Store custom NPM Packages in Azure Storage and install the modules from there.

## Build Process

Build process should run 'npm install'.

Optional: Consider using the npm script 'postinstall' to run more build tasks for the app.

## Deployment Tasks

Post-deployment tasks to consider:

- Automate deployments.
- Manually deploy part of the app.
- Manually verify files on the host service.
- Manually swap slots.

### Automate Deployments

- GitHub Actions, Azure Pipelines.
- Other CI/CD Processes.
- CLI Tools like Azure CLI, Git, and GH CLI allow pushing to remotes from local.
- Dev Environments: Visual Studio, VS Code enable authenticating to Azure hosting environment (e.g. App Service) and pushing files from within the IDE.

### Verify Files

This can be done in Azure Portal or via VS Code.

### Partial Deployment

Use Azure SSH or bash in-browser portals or VS Code 'files' to remove or add files to an existing deployemnt.

### Slots

If in a paid Subscription and Tier, Slots can be used to Blue-Green deploy in real time including reversing deployments and showingn temporary messages to site visitors.

### Code Deployment Sources

VS Code can deploy a local folder to an App Service. This uses a ZIP file to package files for transport.

Zip Deploy actions include:

- Create Zip Package.
- Onyx Build.
- Node.js Platform detection.
- Manifest File creation.
- NPM Install execution.
- File-copy to `/home/site/wwwroot/`
- Post-run cleanup.

GitHub can be used as a deployment source.

## Application Insights

### Azure Monitor

Integrated with App Service.

Provides monitoring data for Applications, Containers, VMs, and "Monitoring Solutions".

Can be integrated with Power BI.

Metric Analytics and Log Analytics are available.

Alerts and Autoscale configurations can be triggered from Azure Monitor.

Can integrate with Logic Apps and Export APIs.

Quotas are also available for CPU, RAM, Bandwidth, and Storage.

### App Service Runtime Logs

Logs available for:

- Deployment.
- Installation.
- Start Up.
- Running Web App.

### Custom Insights Logging

Use `.traceTrace()` method to leverage this within the application code.

See subsection "Custom Application Insights Logging" [from the learn.microsoft.com module](https://learn.microsoft.com/en-us/training/modules/javascript-deploy-expressjs-app-service/use-app-review-logs) for sample code.

Review 'package.json', 'start' script line for DEBUG setting. Express.js and Node.js support 'DEBUG' variable as a was to enable debug logging in the Web App.

### App Insights in Azure Portal

Settings > Application Insights > View APplication Insights Data > Investigate > Failures

## Tips

Right click your Web App in the Azure Extension and select "Browse App" to launch a Web Browser directly to your deployed app.

Restart the WebApp by right-clicking the App Service resource and select "Restart".

## Resources

Deploy a [Node.js and MongoDB Web App](https://learn.microsoft.com/en-us/azure/app-service/tutorial-nodejs-mongodb-app) to Azure.

[MSFT Azure NodeJS Server Samples Repository](https://github.com/Azure-Samples/msdocs-javascript-nodejs-server).

## Footer

Return to [conted index](./conted-index.html)

Return to [ROOT README](../README.html)
