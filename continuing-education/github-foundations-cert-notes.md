# GitHub Foundations Certification Training Notes

These will be limited reference notes related to the GitHub Foundations Certification learning topics, leading to an exam by the same name.

## Table of Contents

- [Search and Organize Repo History using GitHub](#search-and-organize-repo-history-using-github)
- [Manage Repo Changes With Pull Requests](#manage-repo-changes-with-pull-requests)
- [AuthN and AuthZ User IDs on GitHub](#authn-and-authz-user-ids-on-github)
- [User ID and Access Management](#user-id-and-access-management)
- [Communication Using Markdown](#communication-using-markdown)
- [GitHub Projects](#github-projects)
- [Github Codespaces](#github-codespaces)
- [Configure Code Scanning on GitHub](#configure-code-scanning-on-github)
- [GitHub Administration](#github-administration)
- [InnerSource Programs](#innersource-programs)
- [Intro to GitHub Products](#intro-to-github-products)
- [Intro to Git](#intro-to-git)
- [References](#references)
- [Footer](#footer)

## Search and Organize Repo History using GitHub

- [x] Find relevant issues and PRs.
- [x] Search history to find context.
- [x] Make connections to help others find info.

### GitHub Overview

- Website with integrated Git SCM tooling.
- Additional tools for submitting Issues (bugs), having discussions (collaboration), documenting projects (Wikis and Markdown), and managing Users and Repositories.
- Reporting a Bug to a project owner should be done by searching the Issues tab for an existing bug report, and filing a new one if the bug hasn't already been reported.
- To contribute to a GitHub Repository, push your changes to a development branch and then create a Pull Request so code owners can review before mergin into the upstream branch.

### Searching GitHub

Use GitHub "Sidebar" (the search box next to the Octocat icon) for results:

- Repositories
- Commits
- Issues
- Discussions
- Packages
- Marketplace
- Topics
- Wikis
- Users

Use Filter Clauses:

- Used by some providers, ignored by others.
- Without any clauses, GitHub Sidebar Search is global.
- There are too many to list (common ones follow).
- `is:open`
- `is:issue`
- `assignee@...`: Specific GitHub user assigned to a WOrk Item.
- `author:...`: Specific GitHub user.
- `in:...`: Area such as comments.
- Specific area of GitHub such as `sidebar` can be used by name.
- `-linked:...`: Linked to a pr, issues, etc.

Context Search:

- Open a GitHub Tabs and use its Search Bar instead.
- Focuses on the context of the Tab e.g. Issues, Pull Requests, etc.

Git Blame:

- Displays Commit History for a file.
- Identify user that Committed and when it was done.
- Commit changes are displayed with the username/id.
- Can be _aliased_ to "git praise" or another command to sound less judgemental.
- Display within GitHub web UI.
- IDE Extensions can also display Git Blame data right in the IDE UI.

Cross Linking:

- Issues, Commits, etc.
- Syntax is: precede with `#` then select from the dropdown a list of Issues, PRs and other GitHub items.
- Use `@mention` to notify the GitHub user they can participate in the discussion, or other work item type.

## Manage Repo Changes With Pull Requests

- [x] Review use of Branches.
- [x] Define and Create a Pull Request.
- [x] Pull Request states.
- [x] Mange Pull Requests to a Base Branch

### Branches and Pull Requests

Branch:

- Isolated workspaces.
- Develop work without impacting other repo workers.
- Experiment with new ideas in a sandbox environment.
- Record a history of Commits.

Merging Branches:

- Work needs to eventually be merged together.
- Usually into a common branch like Main.
- Many Commits and Merges are tracked into Main or another common branch.
- Tracking multple Merges is done through Pull Requests.

### Pull Requests (PRs)

Can be done:

- In the GitHub Web UI.
- Within an IDE that supports Git natively or through an extension or plug-in.
- Git or GitHub command line.

What they do:

- Document branch changes between developer's branch ("compare branch") and the branch the changes are set to get merged into ("base branch").
- Branches that have the same Commit History cannot be used to create a Pull Request.
- Enable commenting, code reviewing, additional Commits, and merging-in to the base branch.
- Can be cancelled with or without any other actions being taken. No changes to base branch are made.

PR States:

- Draft: Cannot be merged and code owners are not automatically notified of the PR existence.
- Open: Notifies code owners that a request to merge-in from a compare branch is wanted. Collaboration between code owners and contributors happens at this stage.
- Closed: Can be done without merging changes, for example if the changes are no longer needed, or if another solution is proposed in another branch.
- Merged: The commit history from the compare branch has been merged into the base branch history.

Type Of Merges:

- Merge Commit: All commits from compare branch are merged-in one by one to base branch history.
- Squash: Treat all commits within the PR as a single Commit that is then treated as a Merge Commit (see above).
- Rebase: Avoids Merge Commit operation and maintains a linear history.

Notes:

- After merging, the PR will be closed and the branch can be safely deleted.
- Add a CODEOWNERS file and enable Required Review on the base branch.

## AuthN and AuthZ User IDs on GitHub

- [ ] AuthN and AuthZ Models.
- [ ] Manage user access to GH Org.
- [ ] ID providers used to secure repo access.
- [ ] Enabling SAML SSO.
- [ ] ID AuthN, AuthZ options and Enterprise enforcement.
- [ ] Describe access to private info in a GitHub organization.
- [ ] Benefits of Team Membership and Team Sync.

## User ID and Access Management

User Authentication:

- Username & Password: Vulnerable but still supported.
- 2FA: Two Factor Authentication _preferred_, and supported by GitHub. Security Keys, TOTP, and SMS are all supported.
- SAML SSO: Also _preferred_. LInks IdP authorization and access to Service Providers by signing-in to another service, like GitHub.
- Accessing repository data might require an Enterprise ID to authorization.

Supported IdPs:

- Active Directory Federation Services (AD FS).
- Microsoft Entra ID.
- Okta.
- OneLogin.
- PingONe.
- Shibboleth.

GitHub has limited support for SAML 2.0 IdPs. Not all SAML ID Providers are supported by GitHub for SCIM.

Repository Administrator Capabilities:

- Produce a CSV of every user and their access rights within a repository.
- Change access levels between Public, Private, or (for Enterprise accounts) Internal.

Common Administrator Tasks:

- 2FA Audit for User Compliance. This setting must be made by each user in their account.
- When 2FA "Require" is set, any non-compliant user will not removed from the GitHub Organization. Admins must communicate the criticality of using 2FA to onboard users ahead of implementation.
- Audit which users have enabled 2FA within your Organization's People, 2FA option.
- Link the existing SAML-SSO to GitHub Enterprise for user sign-in management. GitHub Org needs to be liked with Enterprise IdP to get started.
- Enforce SAML SSO settings for the organization using GitHub Organization Settings tab, Organization Security, and select "Require SAML SSO authentication for all members of the organization". Note: This will kick-out members that have not set their accounts to sign in using SSO yet.
- Invite others to join the Organization, once SAML SSO is enabled.
- Acquire Administrative Access or a Liaison to enable Team Synchronization between GitHub and the IdP used in your organization.

PATs, SSH keys, and OAuth Apps:

- SCIM: System for Cross-domain Identity Management. Add, manage, and remove Org member access within GitHub. Also synchronizes information with IdP and multiple applications.
- Automatic Deprovisioning: Enabled only when SCIM is implemented. Synch-able changes include Users, Group Membership, Teams, and "Dynamic Config".
- PATs: Personal Access Tokens. Must be authorized with use in SAML SSO configuration.
- SSH Keys must also be authorized for use in SAML SSO configuration.

GitHub Support Out-of-scope Topics:

- Third-party integrations.
- Hardware setup.
- CI/CD e.g. Jenkins et al.
- Writing scripts.
- Config of external Authentication systems e.g. SAML ID Providers.
- Open-source projects.

Usage Limits:

- GitHub Teams: 5k members
- GitHub Organization: 10k members and 1,500 Teams

Terminology:

- IdP stands for "Identity Provider".
- TOTP App: Time-based One Time Password software.
- Dynamic Config: Setting figures out mappings between Active Directory metadata and GitHub settings.

## Communication Using Markdown

- [x] Add lists, images, and links to a Comment or text file.
- [x] Know where and when to use MD in a GH Repo.
- [x] Syntax Extensions in GitHub-flavored Markdown.

### Overview

Provides convenient way to style text without the overhead of full HTML.

- Emphasize text with Bold and/or Italics
- Declare Headings 1 through 6
- Link to Images and Sites
- Ordered and Unordered Lists
- Tables
- Quote Text
- Breaks (gap-filling)
- Code fencing with ` and ```
- Cross-link Issues and PRs
- Link Specific Commits
- `@`Mentions Users and Teams
- Track Task Lists
- Slash Commands (see below)

### Allows Inline HTML Anyway

Want to use HTML anyway? Do it! `<b>Hello</b> <em>World</em>!` renders as: <b>Hello</b> <em>World</em>!

_Note_: Your linter might not like this.

Key takeaway: Just inline any desired HTML.

### Details

- Emphasize text: `*`_italic_`*` (preferred) or `_`_italic_`_`
- Bold: `**`**bold**`**` (preferred) or `__`**bold**`__`
- Bold Italics: `_`_`**`**Italic and Bold**`**`_`_`
- Delimit markdown characters so they are displayed instead of rendered: `\`. For example, display an underline bookended with asterisks: \*\_\*
- See [markdownlint Rules](https://github.com/DavidAnson/markdownlint/blob/v0.36.1/doc/Rules.md) for some tips using well-formed markdown (but not GitHub Markdown specific).

### Slash Commands

- `/code`: Markdown codeblock.
- `/details`: Collapsible detail area with Title and Content (accordian-like).
- `/saved-replies`: Inserts a Saved Reply or use `%cursor%` to put a cursor in that location.
- `/table`: Insert a table using MD.
- `/tasklist`: Insert a tasklist _only within an Issue Description_.
- `/template`: Show all Issue and PR Templates in current Repository and choose the one to insert.

## GitHub Projects

Overview: Create Issues to drive Task creation and completion, relate work items and PRs, customize Fields, and enable Conversations (collaboration).

- [x] Differentiate Projects and "Projects (Classic)"
- [x] Build an Org-level Project
- [x] Organize the Project
- [x] Edit visibility, access, and management of the Project
- [x] Develop project-level automation and insights

_Note_: Projects can be Closed and Deleted.

- Close: Removes from list of Projects but content in retained. _Can_ be opened later.
- Delete: Permanent removal from the platform including Views, custom Fields and values, Insights, and Drafts.

### Projects vs. Classic

| Category/Feature | Projects | Classic |
|----------|----------|----------|
| Boards | Yes   | Yes   |
| Lists | Yes   | No   |
| Timeline Layout | Yes   | No   |
| Sort, Rank, Group tabular data | Yes | Columns and Cards   |
| Create visuals and charts | Yes   | No, just a progress bar   |
| GraphQL API | Yes | No |
| GitHub Actions | Yes | No |
| Column Presets | Yes | Yes |

### Tables and Boards

- Plan and track work.
- Rank, sort, group by any custom field.
- Draft issues with descriptions, metadata.
- Tokenized filtering, saved views.
- Customizable cards and groupings.
- Indicators of project state, progress.

### Data

- Custom fields with Types (e.g. Number, Date, etc).
- Iterations: Flexible date ranges, breaks, springs, cycles, and roadmap.
- Linked PRs, reviewers in table and board views.

### Insight

- Create, config custom bar, column, line, and stacked charts.
- Aggregate data: Sum, Count (etc).
- Persist Charts: Static URL for sharing.

### Automation

Common Automation Tasks:

- GraphQL ProjectsV2 API
- GitHub app Project scopes
- Webhooks events for metadata updates
- GH Action to automate adding Issues

Ways to automate:

- Built-in automated workflows: Simplest option. New Issues and PRs are put into TODO status.
- GraphQL API: Trigger on Push or Scheduled, or setup 3rd Party or GraphQL CLI operations.
- GitHub Actions with workflows: Example: On Issue Creation add Label, add Comment, Move to a specific Board.

### Create a Project

Org-level Creation:

1. Your Organizations
1. Overview
1. Projects :arrow_right: New Project
1. Select template (or not)
1. Select Table
1. Click Create Project

### Project Properties

Common Props:

- Project Name (auto-saves?)
- Short Description
- README: This is displayed as the _Project Readme_ similar to how README works for a single Repository

### Common Tasks

Overall: Use the "+" sign to add new things within the Table including Fields:

- Copy Issues and PRs: Copy existing URL and paste into new item in Project table.
- Search: Existing Issues and PRs. Search tool updates while typing search term(s).
- Bulk Add (Issues and PRs): "+" sign allows selecting a Repository to choose from.
- Create Field to track and group priority.
- Add iteration Field(s). Remember to add start date and duration.
- Create a Board View. Built-in Layouts are available. Rename the View when done creating.

### Organize Your Project

Field Types: Text, Number, Date, "Single select", and Iteration:

- Text
- Number
- Date
- Single Select: Allows multiple options, each with description and color, for a drop-down menu UX.
- Iteration: These help plan upcoming work and help to group items by setting start dates and durations.

Project Visibility and Access:

- Visibility can be Private or Public.
- Organization-Level Project: _No access_, Read, Write, or Admin.
- Personal/User Project: Read, Write, or Admin.

Invite Collaborators: Invite individuals via Search then update their Role to supply the correct access permissions.

### Add Project To A Team

Teams are granted REad Permissions on any Project they are added to.

1. Open Your Organizations and select the target Org.
1. Open Teams tab and select the Team to grant access to.
1. Select Projects and choose "Link a project" to search for and select the target Project.

### Add Project To A Repository

Can only list Projects if same User or Organization owns _both_ the Projects _and_ the Repository.

How to (Visibility is required):

1. Main repository page select Projects tab.
1. Click "Link a project" to search for Projects owned by the same User or Organization as the Repo Owner.
1. Select the Project.

### Project Insights

View, create, and customize charts based on Project Items:

- Filters: Limit results to particular assignees or labels.
- Chart Types
- Information Display
- Current Data: Show items by assignment and iteration or individual.
- Historical Data: Available to GitHub Teams and GitHub Enterprise Cloud for Organizations. Time-based focused on trends and progress. Includes "Burn Up" chart.

Create: Within the Project "Insights" label, select new Chart and pick a chart type using the filter.

Customize:

1. Select the chart to edit.
1. Select Configure.
1. Select Layout to pick a new Chart Type.
1. Select X-axis to select appropriate Field.
1. Select Group-by for the select Field, or None.

## Github Codespaces

- [x] Codespaces lifecycle and processes.
- [x] Customize Codespaces at startup.
- [x] Codespaces vs. GitHub.dev

### Codespaces Overview

Codespaces in a cloud-based IDE with all the tools and functionality of VS Code and the ability to interop with GitHub Repositories and JetBrains IDEs.

- A GitHub account is required and a billing account is necessary to enable Codespace usage.
- Codespaces puts a clone of the source Repository into its `/workspaces` directory.
- Usage of a `devcontainer.json` file will enable pre-configuration of a CodeSpace as defined in the JSON.

### Codespaces Costs

Monthly Included Storage and Core Hours for Personal Accounts:

- GitHub Free: 15 GB/month and 120 Hrs.
- GitHub Pro: 20 GB/month and 180 Hrs.
- Paid usage break-down is complex but for a 2-core configuration used for 1 hour will incurr $0.18 charge.
- Billing and limits to creating additional Codespaces is strictly by Storage and CoreHours usage limitations, not number of Codespaces per Repo, etc.

Some open-ended questions:

- [x] How to monitor usage? Open your profile settings and navigate to Billing :arrow_right: Summary to see limits and monthly usage report.
- [x] Cost after surpassing 60 hours? Since asking this question the Free Hours has been double to 120/month. See bullet points above for more costs info.
- [x] What features are included in CodeSpaces? Fast spin-up, customizable using codespaces file and `.vscode` settings file. Also template-able for consistent new Codespace configuration spin-up.

### Codespaces Lifecycle

Designed to create a repeatable develpment enviornment configured for a project.

- Lifecycle begins at startup, ends at deletion.
- Disconnect and reconnect does not affect running processes.
- Stopping does not lose changes to files and configuration.

### Create a Codespace

Create via GitHub.com, VS Code, or GitHub CLI.

Launch Codespace from:

- GitHub Template or templated repository.
- Branch in your repository.
- An Open PR.
- Specific Commin in a repository's history.

Codespace Creation Process:

1. VM and storage are spun-up.
1. Container is created.
1. Connection to Codespace is initialized.
1. Post-creation steps are executed.

Saving Changes:

- Web: Autosave is enabled.
- VSCode: Autosave is _avaiable_ but must be enabled, if wanted.

Supported Apps:

- VSCode
- JetBrains IDE
- GitHub CLI
- Web browsers

Inactivity Timeouts:

- Saved and shutdown after 30 minutes.
- Personal Timeout setting can be configured.
- Organizational Timeout settings may override Personal Timeout setting.
- _Stopped_ Codespaces are _deleted after 30 days_ automatically.

Internet Connectivity Required:

- Spotty connections or poor bandwidth o.k. but save often to safegaurd from lost data.

### Close or Stop a Codespace

- Exit Codespace without running Stop Command allows Codespace to _run in the background_.
- Timeout timers start when disconnected while Running.
- Disconnect leaves Codespace running but saves changes including uncommitted (but does not commit for you).
- Restart has same behavior.
- Go to the [CodeSpaces Dashboard](https://github.com/codespaces) and find the CodeSpace to clean up and click the Delete button.
- At the very least, 'Stop' the CodeSpace until you need it next.

### Rebuild Codespace

- Allows changing the underlying configuration.
- User-data is saved and restored after restarting the Codespace.
- Full Rebuild: Clears all cached info. Slower restart process but ensures clean startup.
- Rebuild causes all data outside of `\workspaces` directory to be cleared.

### Delete a Codespace

After pushing changes (or you are ready to abandon them), delete the Codespace.

- Non-recoverable operation.
- Unpushed commits will cause a warning, verification prompt before deletion.
- Uncommitted changes are lost.

### Codespace Personalization

A dedicated environment that is configurable:

- Settings Sync: With VS Code!
- Dotfiles.
- Rename Codespace: Overwrite auto-generated name.
- Change Shell: Can be configured manually or through dotfiles.
- Change Machine Type: Use correct resources to get the job done.
- Default Editor: VS Code Desktop, VS Code Web Client, JetBrains Gateway, JupyterLab web.
- Region: Stores data according to your configured region.
- Timeouts: Personal settings and Organizational settings.
- Automatic Deletion: Default 30 days, can be adjusted (max 30d).

Extensions and Plugins:

- Visual Studio Marketplace Extensions are supported.
- Settings Sync: Automatically sync your settings to this Codespaces instance.
- JetBrains Marketplace support.

### What About GitHub.Dev Editor?

Both Codespaces and GitHub.Dev do basic branch viewing and code editing.

Codespaces has these additional features:

- Build and run code.
- Terminal access.
- Costs after free monthly quota.
- Container spin-up delays but with VM Container compute available during use.
- Full Extension support (GitHub.Dev is limited).
- A project being worked on in GitHub.Dev can be "continued with..." Codespaces.

### Codespaces Limitations

- Internet connectivity is required. Although, disconnection from the Internet will not change the CodeSpace state. After a timeout, the CodeSpace will be shut down but all changes will be store _within the Codespace itself_ (not committed to any branch).
- Billing is required. A paid GitHub user will gain access to CodeSpaces and a spending limit can be set and enforced.

## Configure Code Scanning on GitHub

- [x] Describe Code Scanning.
- [x] Enable Code Scanning in a Repo.
- [x] Enable 3rd Party Analysis settings.
- [x] Contrast CodeQL in GH Actions vs. 3rd Party CI tools.
- [x] Explain Triggering Events in Repo Code Scanning.
- [x] Contrast scheduled vs event-triggered Code Scanning.

### Code Scanning Purpose

Find security vulnerabilities and coding errors.

- Available for all public repos and private repos owned by Orgs where GitHub Advanced Security is enabled.
- Code Scanning triggers Alert in Repo's Security tab when vulnerability is found.
- Code fix that removes the vulnerability or error automatically closes the Repo Alert.

### Code QL

The engine behind Code Scanning.

Setup CodeQL Analysis:

- Use default setup to get going quickly. Chooses languages to scan, queries to run, events to trigger, and creates a GH Action to handling it all for you.
- Use Advanced setup to add CodeQL directly to Repo.
- Customizable Workflow is generated by using `github/codeql-action`, then is run as GitHub Action.
- Use CodeQL CLI directly: Generate results then upload them to GitHub yourself.

Supported Languages:

- C/C++
- C#
- Go
- Java/Kotlin
- JavaScript/TypeScript
- Python
- Ruby
- Swift

CodeQL Default Setup:

- Code Scanning is found in Repo's Security tab.
- Select Default for quick-start with basic options and GH Action workflow auto-generation with alerts.
- Select "Enable CodeQL" to enable scanning.

GitHub Actions Billing:

- Code Scanning uses GH Actions minutes.
- GH Actions minutes are free for public and self-hosted runners.
- Private repos have included limits on time and storage, and billing is applied at each GH Account.
- Monthly Spending Limit: If set, will block GH Action from running once USD threshold is met.
- Invoiced Accounts will have an _unlimited spending_ charge.
- Minutes reset each month.
- Storage does not reset, it is tracked on an on-going basis.

### Enable CodeQL with 3rd Party Tools

Perform analysis elsewhere, then upload the results separately:

- Use Static Analysis Results Interchange Format (SARIF) files.
- SARIF v.2.1.0 or newer is _required_.
- Non-SARIF files will _not_ trigger GH Actions Alerts.

### Code Scanning API

- Accessible over HTTPS at `api.github.com`
- GH API Data Type is JSON.
- GH REST API Custom Media type: `application/sarif+json`
  - Other media types might be in use by 3rd Party apps and APIs.
- Analysis Endpoint: `/analyses/{analysis_id}`
  - Subset of actual data in an analysis is returned.
  - Response includes `github/alertNumber` and `github/alertUrl` properties.
- Data is formatted in SARIF v.2.1.0

### CodeQL CLI

Standalone code analysis product:

- Generate DB representing codebase.
- Query DB interactively to get SARIF-compliant result sets (for upload to GitHub.com).
- Free to use on public repositories at GitHub.com.
- Available for private repos of GH Customers with Advanced Security license.
- There is a bundle of tools available for download from GitHub.

CodeQL Tools Bundle:

- CodeQL CLI.
- Queries and Libraries tools.
- Precompiled queries.

The Bundle is more effecient than using separate downloads and repo cloning.

### Code Scanning with GH Actions

1. Create a GitHub Actions workflow.
1. Set a trigger to automate execution on either `push` or `scheduled` events.
1. Store in `.github/workflows` directory.
1. Use the `upload-sarif` action from the `github/codeql-action` repo.
1. Configure upload-sarif action with input parameters as necessary, such as `sarif-file`: A file or directory where SARIF file(s) will be uploaded (relative to root).

### SARIF Upload Limitations

- Max 10 MB for gzip-compressed. Any more and gzip is _rejected_.
- Up to 5000 results per upload will be processed, rest are ignored.
- Focus SARIF upload contents to the most critical queries (not everything).

### 3rd Party SARIF Generation And Usage

SARIF File generation can be done via other tools besides GH Actions or the CodeQL CLI:

- External Repo workflow output artifacts.
- Set a GH-Action `sarif_file` input parameter with value `sarif-output` to grab the data.

### Upload SARIF File As Part of CI Workflow

- Set GH Action property `upload-sarif` as a step _after_ running CI tests.
- [GH Starter workflows](https://github.com/actions/start-workflows) are available.

Example: Running an ESLINT static analysis tool can be output to a SARIF file which can then be uploaded via the `upload-sarif` action!

### Configure Code Scanning

Configure Default or Advanced Code Scanning:

- Configure setups by entering the Code Security and Analysis settings.
- CodeQL Workflows are stored in `.github/workflows` by default.
- Default file is named `codeql-analysis.yml`

_Remember_: Editing a Workflow requires a Git Commit to set the changes in the repo.

Scanning Frequency:

- On a schedule.
- On the triggering of named events (e.g. push).
- Specify within an existing GH Action YML file.
- Scan On Push: Default. Yaml: `on:push` event. Workflow _must be in the specified branch_.
  - Alerts are automatic.
  - Results appear in Security Tab for the repository.
- Scan on PR: Yaml: `on:pull_request`.
  - Targets default branch.
  - Can target private fork if "Run workflows from fork pull requests" is set in repo settings.
  - Results show in PR Check results.
  - For effeciency: Set these for _merge_ commits and _not_ head commits.
- Use a CRON (see example below).

```yaml
on:
  push:
    branches: [main, protected]
  pull_request:
    branches: [main]
  schedule:
    - cron: '20 14 * * 1'
  ...
```

Define Severities:

- Necessary to identify cause of PR Check Failures.
- Default: On `Error`, `Critical`, or `High`
  - CodeScanning continues.
  - Merging PR is _blocked_ on these codes.
- Repository Settings Tab, Code Security And Analysis: Code Scanning Alerts displays PR failures and alert severities here.
  - Also set Protection Rules to define "Check Runs Failure Threshold".

Avoid Unnecessary PR Scanning:

- Update Code Scanning workflow to ignore or select paths.
- Use `on:pull_request:paths-ignore`
- Or `on:pull_request:paths`
- Use blob-pattern to match dir and filename patters.
- Use an array to define sets of matches (see example below).

```yaml
on:
  push:
    branches: [main, protected]
  pull_request:
    branches: [main]
    paths-ignore:
      - '**/*.md'
      - '**/*.txt'
      ...  
```

### Lab Notes

- CWE: Common Weakness Enumeration. A categorization system of hardware and software weaknesses and vulnerabilities.
- The Security Tab on the Repo page will have a Number in it when there are alerts to review.
- "Indentify": To add indentation as a means to _highlight code_.

## GitHub Administration

- [x] Summarize org structures.
- [x] Summarize permissions levels.
- [x] Summarize how to control access and security.
- [x] ID technologies that enable securing and centrally managing repo access.
- [x] ID technolgies to centrally manage teams and members using directory information services.
- [x] Summarize ho to use GitHub as an ID provider for AuthN and AuthZ.

### Team Level Administration

Users:

- Organization members.
- Can be added to a team.

Teams:

- Create within an Org.
- Can have cascading access permissions applied to them.
- `@mentions` apply to teams.

Identity Provider Compatibility:

- Microsoft Entra ID.
- GitHub Team can be synchronized with a Directory services like Entra ID.
- Onboard new members, Grant new permissions, and Remove access to the GitHub Organization via Entra ID.

Permissions:

- Repository Admin and Team Maintainer have similar permissions assignments.
- Create or delete or rename Team.
- Select or change a Parent Team.
- Add or remove Org members from team.
- Sync GitHub team members with an Identity Provider Group (like a group within Entra ID).
- Add, remove outside collaborators (consultants, temporary employees, etc).
- En/Disable Team Discussions on the Team Page.
- Change Team visibility within an Organization.
- Manage automatic code review assignment for PRs.
- Utilize GitHubs review assignment routing algorithm.
- Schedule reminders.
- Set Team Profile picture.

Team Level Administration Best Practices:

- Use nested teams.
- Create teams based on technology or interests.
- Populate Teams in GitHub Organization in way that reflects company hierarchy.
- Enable team sync between Identify Provider and GitHub.

Admin at Organization Level:

- Owners have wide capabilities.
- Invite and remove users.
- Organize users into a team and grant 'maintainer' permissions to org members.
- Add or remove outside collaborators.
- Grant repo permission levels to members and set baseline permissions to a repository.
- Setup org security
- Setup billing or assign a billing manager for the Org.
- Execute custom scripts against the Org repos including migrations.

Org Best Practices:

- One Org for users and repositories.
- Orgs cannot be easily duplicated.
- Additional costs might be incurred using multiple Orgs.
- Added complexity managing multiple Orgs.

Enterprise Level Administration:

- Includes GitHub Enterprise Cloud and Enterprise Server instances.
- Owners have vast permissions.
- Enable SAML SSO at Enterprise Account and allow GitHub users to link their external ID.
- Add, remove Orgs from Enterprise.
- Set up or delegate Billing management for Org in the Enterprise.
- Set policies for: Repo management, project boards, teams, and other security settings at all Orgs and repos and members of the Enterprise.
- Execute custom scripts against all orgs including Enterprise migrations.

The Most Common Administrative Task: Setup and Control User Authentication to GitHub.

- Encourage users to move away from "Basic"(http) auth methods.
- Enable, use Personal Access Tokens (PATs).
- Enable, use SSH Keys. Note: SSH Keys _can_ be used to authenticate against an Org's SAML SSO, or if the Org provides SSH Certificates.
- Enable, use Deploy Keys: Applies to a single repository, rather than a GitHub User Profile or Organization. Default permission is "Read-Only" but can be configured with "Write" permissions.
- 2FA: Can be set as _required_ for an entire Org. Leverages SMS or GitHub Mobile for the second factor.
- Enforce certain security policies for all Orgs owned by an Enterprise account, such as making 2FA required.
- SAML SSO: As part of central ID management, allows securing access via the Organization's IdP. User gets redirected after authentication to the requested resource. Can use Active Directory/ADFS, Microsoft Entra ID, Okta, OneLogin, or PingOne.
- LDAP: Allows authenticating GH Enterprise Server against existing accounts to centrally manage repo access. Very common. Services include: Active Directory, Oracle Directory Server Enterprise Edition, OpenLDAP, and Open Directory.

Repository Permission Level:

- Permissions can be assigned at the repository level.
- Read: non-code contributors.
- Triage: Contributors managing Issues and/or Pull Requests.
- Write: Allows pushing commits to the repo.
- Maintain: Manage repository without making "destructive changes".
- Admin: Full access to project including sensitive info. Are repo owners and admnistrators.
- Template these repository settings so they can be applied to other repos

Team Permission Levels:

- Assign repo levels to related users all at once.
- Permissions inheritance set parent's permissions to child team(s) (cascading).
- There are only TWO permission levels: Member (same perms as Org Member), and Maintainer (maintain team-level settings).

Organization Permission Levels:

- Owner:
- Member:
- Moderator:
- Billing Manager:
- Security Managers:
- Outside Collaborator:

Enterprise Permission Levels:

- Owner:
- Member:
- Billing Manager:
- Permission Levels must be set (default is "No Policy");

Repository Security Management:

- Create Protection Rules.
- PR, Status Checks Pass, or Conversation Resolution before Mergin.
- Require signed commits, linear history, or merge queue.
- Deployments must succeed before merging.
- Read-only "locked" branch.
- Restirct who can push to matching branches.

CODEOWNERS File:

- Part of repository security management.
- Assigns named members as persons responsible for code in the repo.
- Enables automatic notifications and sets Reviewer(s) with new PR creation.
- Place CODEOWNERS file in root, or docs, or `.github` directory.

Insights:

- Repository-level graphs and tables.
- Statistics on Pulse, Contributors, Traffic, Commits, Code Frequency, Dependency Graph, Network, and Forks.
- Traffic statistics for Clones and Views are also available.

## InnerSource Programs

### Inner Source Key Points

- InnerSource are like Open Source programs except access is limited to people within the Organization.
- Use Issue Templates that are designed to encourage descriptive Issues with reproduction steps, attached images or logs, and system details such as OS or platform, configuration, and other helpful details.
- A successful InnerSource program metric is an increase in contributions including PRs and feedback on teh program.

### InnerSource Read More

[InnerSource0-easuring Success](https://github.com/resources/articles/software-development/innersource#measuring-success)

## Intro to GitHub Products

Remember:

- Git is used locally to track and store changes and GitHub can act as a remote repository in a DVCS.
- GitHub provides additional features around Git and project management, useful to individuals and to groups and organizations.

### Personal, Organizational, and Enterprise Accounts

Personal:

- Every user that signs-up for an account has a Personal "user" account.
- Accounts own resources: Repos, packages, projects, etc.
- Permissions can be applied to a personal account.

Free vs. Pro:

- Both allow _unlimited public and private repositories_.
- Both allow _unlimited collaborators on those repositories_.
- Free: Private repos owned by personal account have limited features.

Organizations:

- Are shared accounts (_not_ individual).
- Act as collaboration hubs for many people across one or more projects, simultaneously.
- Tiered approach to permissions.
- Does _not_ support sign-in (users do not sign-in to Organizations).
- Personal accounts can be members of multiple Organizations.

Enterprise:

- Administrators centrally manage policies and billing for multiple Organizations.
- Inner-sourcing within and between organizations is allowed.
- An Enterprise Account has a handle, just like a user account does.
- Manage and enforce policies for all owned Orgnaizations.
- Policies are applied at a per-Organization level.
- Centrally manage users and repos across multiple organizations.

### GitHub Plans

GitHub Free:

- Individuals and Organizations.
- Anyonen can sign-up.

Free Personal:

- Community support
- Dependabot alerts
- 2FA enforcement
- 500 MB Pcakages storage
- 120 Hrs Codespaces per month
- 15 GB Codespaces per month
- 2k Github Actions per month
- Deployment protection rules for _public repos_

Free for Orgs:

- All Free for Personal features.
- Team access controls for managing groups.

GitHub Pro:

- GitHub support via email
- 3k Actions/month
- 2 GB Packages storage
- 180 Hrs Codespaces/month
- 20 GB Codespaces storage/month
- Advanced tools: Require PR Reviewers, multiple PR reviewers, protected branches, code owners, GitHub Pages, Wikis, Repo Insight Graphs

GitHub Team:

- Adds more Actions minutes
- Adds more Packages storage
- Other features: Draft PRs, Team PR reviewers, scheduled reminders
- Manage access permissions to repositories among members of a GitHub Organization, by assigning roles to different Groups.

_Think of this as_ a subset of a GitHub Organization, created to assign permissions based on team membership _within the Organization_ and perhaps modeling an actual business team structure.

GitHub Enterprise:

- GitHub Enteprise Support
- More security, compliance, deployment controls
- SAML and SSO authentication
- SAML or SCIM access provisioning
- Private repot deployment protection and rules for GH Actions
- Option to purchase "GitHub Advanced Security"
- Options: GitHub Enterprise Server; GitHub Enterprise Cloud :right-arrow: Each increases Actions/month, Package storage, adds an SLA, and allows for central management of multiple Organizations, as well as managing users via "Enteprise Managed Users" accounts

### GitHub Mobile and GitHub Desktop

Mobile:

- Manage Notifications
- Read, review, collab on Issues and PRs
- Edit files in PRs
- Search, browse, interact with Users, Repos, and Orgs
- Get PR notifications through _mentions_
- Schedule Push Notifications (do not disturb hours etc)
- Enable and use 2FA with GitHub.com
- Verify sign-in attempts

Desktop:

- Add, clone repos
- Interactive Commit changes
- Add coauthors to Commits
- Check-out branches with PRs
- View status of Continuous Integrations
- Compare changed images

### GitHub Billing and Payments

Bills are specific to each account: Personal, Organization, Enterprise.

Billing Charges:

- Subscriptions: Pro or Team and other paid products such as Copilot.
- Usage-based: Hours and Storage utilization beyond free allocations/period.

## Intro to Git

Version Control is:

- VCS for short.
- Tracks changes to a collection of files.
- Can easily recall earlier versions of one or more files or an entire project.
- Collaboration among many to edit files synchronously, or asynchronously.
- SCM: Software Configuraiton Management. Somewhat interchangeable with VCS. Remember `git-scm`?
- Track who made what changes, and when.
- Captures comments about committed changes, including justification.
- Branching: Experimental changes won't affect the main branch line or other editors.
- Tagging: Add descriptive flags such as a version number or release info.

_Note_: Git was created by Linus Torvals (creator of Linux).

Distributed Version Control Systems:

- Centralized VCS systems like CVS, SVN, and Perforce used a single-server system.
- Git uses history stored both on client and server systems and so is _distributed_.
- Working Tree: Set of directories and files containing a Project.
- Repository: Directory at the top-level of a Working Tree.
- Bare Repository: _Not_ part of a working tree. Often used for file-sharing outside of a Git Repo.
- Hash: Number that represents the contents of a file or other object. Used as reference points in Git.
- Object: Blobs (files), Trees (directories), Commits (specific version of a tree), Tags (a name attached to a Commit).
- Commit: Two meanings:
  - Verb: To make a commit object.
  - Noun: Specific version of a tree (a current state).
- Branch: A named series of linked commits.
- Head: Most recent Commit on a Branch.
- Remote: The named reference to another Git repository. Default name is 'origin' but custom names can be created. Multiple remote refs can be created per Repo.
- Commands, Subcommands, and Options: Used to perform actions within a Working Tree such as 'merge', 'branch', 'commit', 'tag', and many more.

Differences between Git and GitHub:

- GitHub is a website with many related tools to support DVCS operations and lifecycle.
- Primary GitHub Features: Issues, Discussions, Pull Requests, Notifications, Labels, Actions, Forks, and Projects.
- Git is a distributed version control system (DVCS) that tracks changes to files.
- Git enables many users to contribute to a project through tools like `branch` and `commit`, and to view other user's code though tools like `checkout`.

The roles Git and GitHub play in SDLC:

- Git provides a local repository to track and store Working Tree changes.
- GitHub acts as the remote repository for DVCS.
- GitHub also has features that assist single contributors and groups of many contributors to manage their software development project and lifecycle.

### Git Repo Startup on Command Line

Set the following:

- User Name: `git config --global user.name "{user-name}"`
- Email: `git config --global user.email "{user@email.example}"`

List existing Git configuration:

- `git config --list`

Create repo:

1. Make a new directory
1. Init git with a default branch named 'main': `git init -b main`

### Common Commands

- Get branch name, commits, and info on staged or changed files and directories: `git status`
- Start tracking changes: `git add {object...}`
- Snapshot changes: `git commit {options}`
- View commit changes and comments: `git log`
- Get help: `git help`

## References

- [Advanced Search configuration](https://github.com/search/advanced)
- [GitHub Codespaces Overview](https://docs.github.com/en/codespaces/overview)
- [Managing Billing For Github Codespaces](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-codespaces/about-billing-for-github-codespaces)
- [GitHub REST API Endpoints for Code Scanning](https://docs.github.com/en/rest/code-scanning/code-scanning?apiVersion=2022-11-28)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
