# Build and Test Node.js with GitHub Actions

## Table of Contents

- [Overview](#overview)
- [Runners](#runners)
- [Workflows](#workflows)
- [GitHub Actions](#github-actions)
- [With](#with)
- [Run](#run)
- [Node-Version](#node-version)
- [Workflow Artifact Storage](#workflow-artifact-storage)
- [Pushing to Package Registries](#pushing-to-package-registries)
- [My Exeperiences](#my-exeperiences)
- [CI With GitHub Actions](#ci-with-github-actions)
- [References](#references)
- [Footer](#footer)

## Overview

GitHub Actions provides Runners with Linux, Windows, or Apple OSes, and supports installing dependencies and executing shell commands to build, test, and deploy node.js apps.

## Runners

GitHub provides 'Runners' that are pre-defined environments used for build, test, and deploy operations.

Runners come with specific minimum capabilities like:

- Yarn.
- npm.

Windows-based runners _also_ have:

- Grunt.
- Gulp.
- Bower.

Runners can cache dependencies to speed up builds.

### Installing Dependencies

- Just like on your local machine, use `npm i` to install dependencies.
- Package.json must be up-to-date and functionally correct.
- After you install dependencies, other apps and shell commands can be available!
- `package-lock.json` and `npm-shrinkwrap.json` are supported.

Commands:

- `npm i`: The usual too.
- `npm ci`: Tends to be [faster](https://blog.npmjs.org/post/171556855892/introducing-npm-ci-for-faster-more-reliable).

_Note_: Private registry installation using `.npmrc` file is supported. Use `setup-node` action to support this feature (required tokens/encrypted secrets).

## Workflows

- Use YAML to define the workflow.
- Store in `.github/workflows` folder in your repository.
- `on`: Defines the Git event that triggers the workflow.
- `jobs`: Defines the work to perform.
- `build`: Name of the job.
- `runs-on`: Defines the OS to run the job on.
- `strategy`: Defines the matrix of Node.js versions to run the job on.
- `steps`: Defines the steps to run in the job.
- `uses`: Defines the GitHub action to run.
- `with`: Defines the parameters to pass to the action.
- `run`: Defines the shell commands to run.
- `env`: Define local environment variables, and cloud-based environment variables and secrets.

## GitHub Actions

- There are GitHub repositories of Actions that can be used.
- Reference them like `uses: actions/setup-node@v3`.
- There are Action predefined for many OSes, build environments, etc.

### Intro To GitHub Actions

GitHub Actions are related to GitHub workflows, events, Jobs, and Runners.

- Primary mechanism for automation on GitHub.
- Most common usage is CI.

GitHub Actions Are:

- Provide workflow automation.
- Enable Test automation.
- Automate responding to new Issues or `@mentions`.
- Enable triggering code reviews.
- Can be set to handle PRs.
- Able to manage Branches in your GitHub repo.

### GitHub Actions Flow

Events trigger Workflows that contain Jobs that use Actions.

- GitHub tracks Events.
- Events trigger Workflows.
- Events can be manually fired.
- Workflows are units of automation containing Jobs.
- Jobs use Actions to get work done.

### GitHub Workflows

Workflows define automation.

- Detail Events that trigger workflow.
- Define jobs that run.
- Defines where actions are executed e.g. which runner to use.
- Written in YAML.
- Stored in `.github/workflows` directory.

GitHub has [Starter Workflows](https://github.com/actions/starter-workflows).

GitHub [Actions syntax](https://docs.github.com/actions/learn-github-actions/workflow-syntax-for-github-actions).

Standard Syntax Elements:

- Name: Options but highly recommended so workflow can be ID'd in the UI.
- On: What Event triggers the workflow.
- Jobs: List of one or more Jobs to execute.
- Runs-on: Which Runner to use.
- Steps: Each runs in-order on the same Runner.
- Uses: List of Actions that need to be retrieved and run.
- Run: Specific command to execute on the Runner such as `npm i`.

Allowable [Workflow Syntax for GitHub Actions](https://docs.github.com/actions/learn-github-actions/workflow-syntax-for-github-actions).

### GitHub Actions Events

These are Events implemented by a Workflow `on` clause.

- Scheduled: When to run as defined by `cron: 'params'` where params is a `cron` definition wrapped in single-quotes.
- Code: For example `[push, pull_request]` for pushes to a branch or creation of a PR. Define the branch(es) this applies to, by name.
- Manual Events: Use the `workflow_dispatch` event and store the workflow in the default branch of the repo.
- Webhook: Triggered when a GitHub Webhook is called.
- External: Events on `repository_dispatch` enabling remote-firing. There are more details that are not covered here.

### GitHub Jobs

Jobs are encapsulated by Workflows, and is a set of steps to be executed in order by a Runner.

- A Runner contains a file system, so all steps use the same FS.
- Job Logs are searchable.
- Artifacts from jobs can be stored.
- Multiple Jobs are run in parallel by default.
- Define dependencies by using `needs: {other_job}` to force synchronous execution instead.

### GitHub Runners

Runners are compute resources.

- Execute GitHub Actions workflows.
- Runners execute Jobs one-at-a-time.
- Build, test, or deploy directly from within the repo.
- GitHub-Hosted: Virtualized/Containerized resources provided by GitHub.
- Self-Hosted: Physical, virtualized, or containerized resources provided by User/Organization for self-service provisioning and managmeent.

_Note_: Avoid using self-service Runners in Public repos. This is a security risk.

Hosted Runners:

- Execute Workflows within GitHub Actions.
- GitHub-managed hardware and resources.
- Auto-scale.
- Pre-configured environment Runners are available.
- Default, built-in tools for each OS are included e.g. grep, find, which, and others.
- There is an SBOM (software bill of materials) available with a complete list of tools for specified Runners.
- Additional software _can be installed_ on a Runner.
- Runtime is limited to 6 hours execution time per Job in each Workflow.
- Workflow runtime is limited to 35 days.
- Runners can only be configured and run by repo users that have permissions to run GitHub Actions.
- Runner environment, OS, software dependencies are all defined within the YAML file.
- Runners are managed and maintained by GitHub, including weekly security patches.
- Free-tier has a limited number of Actions minutes. Additional costs or licensing fees are necessary beyond those limited minutes.

Self-Hosted Runners:

- Allow greater controly and customization.
- Wider range of environments can be supported.
- Deployment can be on-prem or in a cloud, so long as network and resources are available.
- All Runner specifications are user-accessible and defineable.
- Use these to integrate with existing infrastructure and tooling.
- There are no time limits on Self-hosted Runners.
- Registration can happen at the single repository level, or at the Organization or Enterprise levels.
- Users are ultimately responsible for every other aspect of Self-hosted Runners including infrastructure costs, and costs of Licensing GitHub Runners.

### Reviewing GitHub Actions Customization And Results

- Logs are available in the repo's Action tab.
- Tags can be used to specify a Action version.
- Specifying a SHA-based Hash will ensure only a specified Action and Version will be executed.
- Referencing a target branch ensures the proper code is selected by the Action.

Training: [GitHub Actions: hellow-world](https://github.com/skills/hello-github-actions).

## GitHub Action Best Practices

Consider contributing to the Actions Marketplace. Follow these best practices when creating Actions for your Repos as any Marketplace contributions:

- Create chainable Actions, not large monolithic ones.
- Version control Actions just like code.
- Provide the `latest` label to always get the latest.
- Add documentation for the repo Actions and workflows you've implemented.
- Add `action.yml` metadata. Include Author, Icon, expected Inputs, and possible Outputs.

## With

Parameters might include:

- matrix.node-version: References a collection Node.js version to use.
- matrix.os: References a collection of OSes to use.
- Written like: `${{ matrix.node-version }}`.
- See `strategy: matrix: node-version: [...]` for the collection of Node.js versions to use.
- Same for OSes.

## Run

Defines the shell command to run:

- If you want to execute npm build (a shell command) then do: `npm run build`.
- Other commands are available including OS-build-in commands.
- OS must have the command available.

## Node-Version

- Collection: `with: node-version: [...]`.
- Single (major) version: `with: node-version: 16.x`.
- Exact version: `with: node-version: 16.2.3`.

## Workflow Artifact Storage

See GitHub Docs [Storing workflow data as artifacts](https://docs.github.com/en/actions/guides/storing-workflow-data-as-artifacts).

## Pushing to Package Registries

See GitHub Docs [Publishing Node.js packages](https://docs.github.com/en/actions/guides/publishing-nodejs-packages).

## My Exeperiences

### Deploying NodeJS to Azure App Service

GitHub Actions:

- Specified a branch that will be deployed, in this case NOT main but 'azure-deploy'.
- Used `env` environment variables to define Webapp Name, Package Path, and Node Version.
- Set `jobs` to `build-and-deploy` running on `ubuntu-latest`.
- Specified `actions/checkout@v2` and `actions/setup-node@v1`.
- Called shell commands `npm install`, `npm run build --if-present`, `npm run test --if-present`.
- Specified `actions/webapps-deploy@v2`, and pointed to the AppName and PublishProfile environment variables.

Environment Variables:

- `AZURE_WEBAPP_NAME`: Name of the Azure Webapp.
- `AZURE_WEBAPP_PACKAGE_PATH`: Path to the package to deploy. In this case `.` (repository root).
- `NODE_VERSION`: Node version to use. In this case `16.x`.

#### Improvements

I can do the following to improve the above build-test-deploy script:

- Use `npm ci` instead of `npm install`.

## CI With GitHub Actions

These notes were generated while reviewing the MSLearn Module "Learn Continuous Integration: GitHub Actions"

Learning Objectives:

- Implement CI with GitHub Actions.
- Use Env Vars.
- Share artifacts between jobs and use Git Tags.
- Create and manage Secrets.

### Mark Relases with Git Tags

Releases are based on Git tags.

- Mark point in history of the repo.
- Commonly assigned as releases are created.
- Usually Tags will contain version numbers.
- Visible in the repo history.

[About GitHub Tags and Releases](https://docs.github.com/repositories/releasing-projects-on-github/about-releases).

### Actions: Environment Variables

GitHub built-inv EnvVars:

- GITHUB_WORKFLOW: Workflow name.
- GITHUB_ACTION: Workflow unique ID.
- GITHUB_REPOSITORY: Repo and owner name e.g. `repo/owner_name`.

EnvVars are passed to Actions in a Step using `env:` marker.

- Indent to the ENV_VAR name then Idenfity the variable: `PROJECT_SERVER: Srvr-Rnr-01`
- GitHub [Environment Variables](https://docs.github.com/actions/learn-github-actions/environment-variables).

### GitHub Actions Secrets

Secrets are Encrypted Environment Variables:

- GitHub Workflows supports up to 100 Secrets regarless of location.
- Size limit is 48 KB, although larger secrets _can_ be stored using advice in GitHub Docs.
- SECRETS are _not_ passed to a Runner when triggered from a Forked Repo.
- `AZURE_WEBAPP_PUBLISH_PROFILE`: Repository Secret that contains the Azure Webapp Publish Profile.
- Only available at Repository and Organization levels.
- Organization access policies can control Secrets access and management.
- Reference within a Workflow using this syntax: `with: db_username: ${{ secrets.DbUsername }}`.
- Reference within Command Line: `- shell: pwsh \n env: DB_PASSWORD: ${{ secrets.DbPassword }} \n...`

Secrets can be used in `if:` conditionals within a Job.

### Actions: Artifacts

Often times artifacts from one Job need to be passed to another Job.

Uploads:

- Files can be uploaded by name, using `actions/upload-artifact`.
- Upload a file or entire folder with a name to a specific path.
- Wildcards are allowed.
- Multiple paths are allowed.

Downloads:

- Download artifacts retreives artifacts by name, using `actionsdownload-artifact`.
- An unspecified directory will default to `pwd` (current directory).

Retaining Artifacts:

- Use `actions/upload-artifact` and specify `with` params.
- Specify how long to keep the artifact by assigning an Integer to `retention-days`.

Deleting Artifacts:

This is done via the GitHub UI.

### Workflow Badges

Use these to show status in a repository.

- Currently passing or failing workflows.
- Generally added to the root README.md file.
- Add them by using GitHub repository built-in URLs.

Example URL: `https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW_FILE}/badge.svg`

Specify a Branch (other than the default branch) by appending `?branch=BRANCH` to the URL.

[Adding a Workflow Status Badge](https://docs.github.com/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge).

## AZ400 Implementing GitHub Actions Notes

These notes were taken while working through the AZ400 exercise.

1. GitHub Repo import other repository: It is not necessary to add credentials for a public repo.
2. Once import is completed, Settings can be entered to change Actions to allow or disable reusable workflows.
3. Create an Azure Service Principal and save it as a GitHub Secret. This requires knowing your SubscriptionID and the target Resource Group name. Save the JSON output.
4. Register the Resource Provider for the Azure App Service using `az provider register --namespace Microsoft.Web`.
5. Open Settings of the GitHub Repo and go to the Secrets and Variables and open Actions to add the Secret by pasting-in the JSON object.
6. Create the workflow YAML that can leverage BICEP to generate a deploy file, and will use the GitHub SECRET created earlier to authenticate to Azur and deploy the service/WebApp/etc.
7. Open Actions in the GitHub Repo, find the Action (probably in-process) and click on it to see its status.
8. Open Azure Portal and open the Resource Group. A GitHub Action, a Bicep template, and the App Service Plan will appear. In the case of a WebApp, a `browse` button will become available to open the WebApp in your default browser.

It is possible to add a Manual Approval to allow (or reject...or ignore) Deployments prior to the GitHub Action triggering the workflow.

- Add the necessary property to the YAML file (TBD).
- Add a Protection Rule that has the GitHub user account(s) that should be allowed to Approve the workflow execution.
- The next time the Action is triggered, a `Review Deployments` button will appear in the Action Status Page in GitHub. Click it to allow, otherwise click Reject button.

## References

- [Build and Test Node.js with GitHub Actions](https://docs.github.com/en/actions/guides/building-and-testing-nodejs)
- NPM Blog [IOntroducing npm ci for faster, more reliable builds](https://blog.npmjs.org/post/171556855892/introducing-npm-ci-for-faster-more-reliable).
- Deploy to Azure App Service [GitHub Action](https://github.com/Azure/webapps-deploy);

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
