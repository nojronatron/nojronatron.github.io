# GitHub Foundations Certification Training Notes

These will be limited reference notes related to the GitHub Foundations Certification learning topics, leading to an exam by the same name.

## Table of Contents

- [Configure Code Scanning on GitHub](#configure-code-scanning-on-github)
- [GitHub Administration](#github-administration)
- [Intro to GitHub Products](#intro-to-github-products)
- [Intro to Git](#intro-to-git)

## Configure Code Scanning on GitHub

- [ ] Describe Code Scanning.
- [ ] Enable Code Scanning in a Repo.
- [ ] Enable 3rd Party Analysis settings.
- [ ] Contrast CodeQL in GH Actions vs. 3rd Party CI tools.
- [ ] Explain Triggering Events in Repo Code Scanning.
- [ ] Contrast scheduled vs event-triggered Code Scanning.

### Code Scanning Purpose

Find security vulnerabilities and coding errors.

Available for all public repos and private repos owned by Orgs where GitHub Advanced Security is enabled.

Code Scanning triggers Alert in Repo's Security tab when vulnerability is found.

Code fix that removes the vulnerability or error automatically closes the Repo Alert.

### Code QL

This engine behind Code Scanning.

Setup CodeQL Analysis:

- Use default setup to get going quickly. Chooses languages to scan, queries to run, events to trigger, and creates a GH Action to handling it all for you.
- Use Advanced setup to add CodeQL directly to Repo. Customizable Workflow is generated: `github/codeql-action` CodeQL CLI is run as GitHub Action.
- Use CodeQL CLI directly: Upload the results to GitHub yourself.

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
- Invoiced Accounts will have an _unliminted spending_ charge.
- Minutes reset each month.
- Storage does not reset, it is tracked on an on-going basis.

### Enable CodeQL with 3rd Party Tools

Perform analysis elsewhere, then upload the results separately.

- Use Static Analysis Results Interchange Format (SARIF) files.
- Non-SARIF files will _not_ trigger GH Actions Alerts.
- SARIF v.2.1.0 or newer is _required_.

### Code Scanning API

- Accessible over HTTPS at `api.github.com`
- GH API Data Type is JSON.
- GH REST API Custom Media type: `application/sarif+json`
  - Other media types might be in use by 3rd Party apps and APIs.
- Analysis Endpoing: `/analyses/{analysis_id}`
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
- Bundle is more effecient than using separate downloads and repo cloning.

### Code Scanning with GH Actions

1. Create a GitHub Actions workflow.
1. Set a trigger to automate execution on either `push` or `scheduled` event occurs.
1. Store in `.github/workflows` directory.
1. Use the `upload-sarif` action from the `github/condeql-action` repo.
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

## Intro to GitHub Products

Remember: Git is used locally to track and store changes and GitHub can act as a remote repository in a DVCS. GitHub provides additional features around Git and project management, useful to individuals and groups.

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

- Shared accounts.
- Collaborate hubs for many people across one or more projects, simultaneously.
- Tiered approach to permissions.
- Does _not_ support sign-in (users do not sign-in to Organizations).
- Personal accounts can be members of multiple Organizations.

Enterprise:

- Administrators centrally manage policies and billing for multiple Organizations.
- Inner-sourcing within and between organizations is allowed.
- An Enterprise Account has a handle, just like a user account does.
- Manage and enforce policies for all owned Orgnaizations.
- Policies are applied at a per-Organization level.

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

- [GitHub REST API Endpoints for Code Scanning](https://docs.github.com/en/rest/code-scanning/code-scanning?apiVersion=2022-11-28)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
