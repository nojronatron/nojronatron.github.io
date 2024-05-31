# Open Source Learnings and Activities

## Table of Contents

- [Index of Plans and Open Source Contributions](#index-of-plans-and-open-source-contributions)
- [Building An Open Source Program Using GitHub Best Practices](#building-an-open-source-program-using-github-best-practices)
- [Uploading OSS Projects Using GitHub Best Practices](#uploading-oss-projects-using-github-best-practices)
- [Secure OSS Repository Using GitHub Best Practices](#secure-oss-repository-using-github-best-practices)
- [About Contributing To Open Source Projects On GitHub](#about-contributing-to-open-source-projects-on-github)
- [Footer](#footer)

## Index of Plans and Open Source Contributions

- [ ] Project [Humanizer](./oss-contrib-humanizer.html).
- [ ] Project [Meshtastic](./oss-contrib-meshtastic.html), see [Issue 155](https://github.com/meshtastic/web/issues/155), PR is in the queue.
- [x] Project [VGTeam Sequence Tube Map](https://github.com/vgteam/sequenceTubeMap), see [Issue 149](https://github.com/vgteam/sequenceTubeMap/issues/149).

## Building An Open Source Program Using GitHub Best Practices

These notes are from my studying a MSFT Learn module with a similar name.

GitHub refers to the [Open Source Guide](https://opensource.guide/starting-a-project/#launching-your-own-open-source-project) and promotes it as a go-to resoruce for OSS program development, maintenance, and accelleration.

### Building OSS Program - Objectives

- Asses an organization's existing open-source efforts.
- Establish goals of an OSS programm.
- Create a repository for the OSS program.
- Abide by existing open-source licenses.
- Choose a license for releasing an OSS Project under.

### What Is Open Source

A visible, inclusive, living project in the developer community.

Gains from the community include:

- Increased velocity of enhancement.
- Injects from the community help improve stability and accelerate bug find-and-squash efforts.
- Provide inputs into new features and capabilities of the project.

Most OSS projects are 'consumed' by developers. As they gain familiarity with the project, they also gain insights into how to improve it, and generally want to contribute _back_ to the project to make it better.

OSS Goals:

- Consumers: Study or use OSS repos.
- Contributors: Actively involved with OSS repos.
- Producers: Build and maintain own OSS repos that others can consume or contribute to.

Process Levels:

- Ad Hoc: No OSS processes.
- Managed: Some documentation and discipline working in OSS environment.
- Defined: Documented, standardized, integrated, with automation.
- Measured: Quantitative management processes in place, and business goals are targets for OSS success.
- Optimized: Continual improvement via incremental change and innovation. Regular attempts to reduce risks of change.

GitHub has created an [Open Source Self-Assessment Tool](https://githubtraining.github.io/oss-assessment/) available to help determine your Org's Process Level and what steps to focus on next.

What To Open Source?

- Project with IP where the benefits of open sourcing outweighs the risks of doing so.
- Project without IP? Does it provide a benefit to the OSS community (and your business)?
- Stable projects with good code quality. Perfect code is not the goal, rather, code that is ready for contribution with little risk of potential contributors walking away from "a mess".
- Can others contribute, without being an employee or partner of your org? Ever aspect of the project will need to be managed by people with access rights to do so.
- Is there available bandwidth for the Org's team to support OSS program? Without owner team support, the project could be doomed to failure.

Designing an Open Source Program:

- Make a steallar README to help contributors understand the project and the flow.
- Include a CONTRIBUTING to explain how to contribute, code styles, and other formalities.
- Include a CODE_OF_CONDUCT to explain behavioral expectations and interactions within the project context.
- Legal should review the [Code of Conduct](https://opensource.guide/code-of-conduct/) to ensure it meets various requirements, including that of the organization itself.

Preparing to Maintain an OSS Repo:

- Evaluate which project could (or should not) be open sourced.
- Setup checklists of work to prepare for open-sourcing the code/project.
- Design a contacts list of internal project-committed team members.
- Create a template starter repository and link it up for the project to start from.
- Develop a Maintainer's Guide for the project that involved parties want to sign-off on.
- Create a communications guide (encompasses READMEs, Contributing and Code of Conduct files).
- Develop an internal FAQ to cover common issues and overview legal subtleties.
- Develop a license policy to ensure OSS projects use correcting licensing type and stay in compliance with it.

### Benefits Of An Open Source Community

Setup for Success:

- Help reduce friction to contributing.
- Enhance contributor's experience.
- Open communication lines with documentation (README, etc), tools (Issues, PRs, etc), and access (to the repositories and the OSS Project maintainers and their organization/company).
- Utilize GitHub `Insights` on the OSS Repo to open discussions between the community and the maintainers, and to get an assessment of community interest and project acceleration.

## Uploading OSS Projects Using GitHub Best Practices

### Uploading OSS Projects - Objectives

- ID where code is stored.
- Intoduce code to a repo.
- Create important Git files.
- ID next steps to manage repo and involve the community.

### Why Do This?

- Version Control.
- Code in the cloud can save on costs vs. storing on-prem.
- Enables collaboration without deploying services from on-prem.

### How To Do This

Initial Questions to Get Started:

- Are there other data that go with the project but are not Code? Bugs in a separate logging system? Plans and architectural documents that need to be included with the OSS repo?
- Are there binary files/artifacts that will need to be stored in an [Git LFS](https://git-lfs.github.com/) or other non-Git storage medium, like spreadsheets, build outputs, or presentations?
- What items need to be in the `.gitignore` file to help enforce version-control policies?
- Are the communications and instructional files ready e.g. README, LICENSE, CONTRIBUTING, and perahps a SECURITY markdown?
- Are there other `.gitattributes` that need to be configured to ensure proper git configuration of LF/CRLF handling? _[Nojronatron]_
- What will be the branching scheme? Remember to name the primary branch `main`.

### GitHub Importer

This converter will import and upload code from other revision systems:

- Subversion
- Mercurial
- Team Foundation Server
- (others not listed)

There is a command-line version, as well as a GUI version.

GitHub Importer is:

- Not suitable for all imports such as: Code on a private network or the tool otherwise cannot access the source.
- Able to match-up commit names with GitHub user accounts during import. This is a fairly manual process within the tool that basically connects GitHub Usernames to source repo commit user IDs.
- Size-limited per file! Remove large files and binaries from your repo before importing, but moving them into a Git LFS service. Alternatively, allow the Importer to find these files and push them to a Git LRS for you.
- Able to set the target repo as Public or Private.
- Able to set any available name for the target repository.
- Able to handle credentials if required for the import process.

Public Email Addresses:

- GitHub users can set their `commit email` as _private_ in their GitHub account.
- GitHub Importer will then match their email to `<username>@users.noreply.github.com`, instead.
- Users without GitHub accounts will have their currently attributed email on the source commit copied by the GitHub Importer tool.

Existing projects can be added to GitHub by using `GitHub CLI`:

1. `git init -b main`
2. `git add. && git commit -m "initial commit"`
3. `gh repo create`: Provides prompts to help user create and push the repo to GitHub.

Prompts include:

- An organization name, if applies.
- Public/private repository.

The [GitHub CLI Manual](https://cli.github.com/manual/gh_repo_create) has much more detail.

Add a Local Repo To GitHub using Git:

1. Create a new repo in GitHub.
2. GitBash from the project root directory: `git init -b main`.
3. GitBash: `git add .`
4. GitBash: `git commit -m 'Initial Commit'`
5. GitBash: `git remote add origin <remote_url>`
6. GitBash: `git remote -v` to verify correct remote was added
7. GitBash: `git push origin main`

Other Migration tools exist including: `git-svn`, `svn2git`, `hg-fast-export`, `git-tfs`, and arguably, the GitHub Repository Import UI.

## Secure OSS Repository Using GitHub Best Practices

Build, host, and maintain a secure OSS repository.

### Secure OSS Repo Learning Objectives

- ID tools and GitHub features to establish a secure dev strategy.
- Enable vulnerable dependency detection for private repos.
- Detect and fix outdated dependencies with security vulnerabilities.
- Automate detection of vulnerable dependencies with Dependabot.
- Add a security policy file.
- Remove a commit exposing sensitive data in a PR.
- Keep sensitive files out of repository.
- Remove historical commits exposing sensitive data deep in your repo.

### Secure Development Tools and Strategy

Strategy:

- Protect against disclosures of private info.
- Information should only be altered or destroyed when appropriate and authorized.
- Authentication is necessary to ensure correct permissions to manipulate repository features, commits, and code.
- Cybersecurity is a constantly evolving discipline requiring ongoing training.
- Create correct, secure code, with only the required features.
- Applications must comply with rules and regulations.
- Add security concepts to every stage of software development, following shift-left, and dev-ops processes.

### GitHub Repository Security Tab

- Security Policies: Deploy a SECURITY.md file to the repository.
- Dependabot Alerts: Send notifcations when there are vulnerabilities or malware in code or dependencies.
- Security Advisories: Privately discuss, fix, and publish information about vulnerabilities within your repo.
- Code Scanning: Find, triage, and fix vulnerabilities and code errors.

[GitHub Security Features](https://docs.github.com/code-security/getting-started/github-security-features).

SECURIY.md File:

- Devs can responsibly disclosing concerns using this file without creating a public incident.
- [Adding A Security Policy To Your GitHub Repo](https://docs.github.com/code-security/getting-started/adding-a-security-policy-to-your-repository).

Security Advisories:

- Publicly disclose a vulnerability once a fix is available.
- Simplifies updating package dependencies and the advisory fix.
- Published Advisories are stored in the Common Vulnerabilities and Exposures (CVE) list, that automates notifying affected repositories.
- [About Repo Security Advisories](https://docs.github.com/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories).

Create a smart, effective .GITIGNORE file:

- Disables committing potentially (or certainly) sensitive data to the repo.
- Blocks API Keys, Environment Variable values, and other unsecured assets.
- Is _not_ fool-proof: It relies on the repository owner to create an effective, wholistic list and to _keep it up to date_ as the repo ages and technology changes.
- The repository root `.gitignore` should have many (or all) of the required entries.
- Child directories in the repo can have their own, overriding `.gitignore` files to alter what gets ignored.
- [GitHub: Ignoring Files](https://docs.github.com/get-started/getting-started-with-git/ignoring-files).
- [gitignore Repository](https://github.com/github/gitignore).

Remove Sensitive Data From Repo:

- `.gitignore` files can be worked around, or are not carefully crafted to catch all potential asset files.
- Always assume that any new commit to the repository is potentially loaded with compromised code.
- An alternate place to put `.gitignore` is in the `docs` directory.

[GitHub: Removing Sensitive Data From A Repo](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository).

Branch Protection Rules:

- Enforces certain workflows complete with success in order for code to push to the branch.
- Denies committing code to the branch without sign-off from others.
- Forces other tasks like code-formatting or tests to run and pass before Commit is allowed.
- [GitHub Branch Protection Rules](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule).

CODEOWNERS File:

- Individuals or an entire team can be marked as the code owner(s).
- Code Owners are required for PR Reviews for any changes to code within their responsible "paths".
- Defines owners using this syntax: `*.js    @js-owner` and `/build/    @octocat`.
- [GitHub Codeowners file](https://docs.github.com/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/about-code-owners#codeowners-syntax).

### Detect And Fix Outdated Dependencies

Repository Dependency Graphs:

- GitHub scans command package manifests (package.json, [and other dependency manifests](https://docs.github.com/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph)).
- A Dependency Graph is generated by GitHub.

Dependabot Alerts:

- Watch dependency graph for you.
- Cross-references target versions with known-vulerable versions.
- Alerts are raised through Dependabot Alerts on the repository.
- Input analysis source: [GitHub Security Advisories](https://docs.github.com/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories#dependabot-alerts-for-published-security-advisories).

Dependabot Dependency Updates:

- Alerts can cause a project dependency to be 'bumped'.
- Bumped dependencies will generate a PR.
- Dependabot will attempt to resolve merge conflicts (current).
- Not all Dependency Update Alerts will result in a PR that can resolve the issue.

Secret Scanning:

- Look for known secrets or credentials committed within the repo.
- Prevents fraudulent behavior.
- Secures integrity of sensitive data.
- Is _on by default_ on public repositories.
- Private repos can be configured by the repo Admin to enable Secret Scanning.
- Notification(s) are sent to the provider of the secret, when detected.
- [Secret Scanning FOr Public And Private Repositories](https://docs.github.com/code-security/secret-scanning/about-secret-scanning).

## About Contributing To Open Source Projects On GitHub

GitHub can help locate open source projects and tasks to contibute to, and there are good practices to follow when contributing.

### Objectives

- Find open source projects on GitHub.
- Create PRs to open-sourced projects.
- Implement best practices communicating with open-source maintainers.
- Find and engage with open source communities.

### ID Where To Help

- Contributing might be easier on projects that you already use.
- GitHub has a search function.
- Search for Issues that have a label "Jump In", "Good First Issue", or "Needs Help".
- Other resources are out there to find OSS projects that need help!

### Get Familiar with the OSS Project

Read the Docs:

- LICENSE file: Get familiar with it and how it might impact your ability to contribute, or what might happen to code you commit.
- README: Read it.
- Read the CONTRIBUTING file for specific instructions from the maintainers.
- CODE_OF_CONDUCT: Contains information on the expected behavior of contributors (and the maintainers).

Review the Issues:

- Many GitHub repos use the built-in Issue tracker. Add `/issues` to the end of the repo URL.
- Some repos will use a 3rd party tool - see the Docs to learn where, if this is the case.
- Check out open PRs. Add `/pulls` to the end of a repo URL to find them.
- Join in Discussions, or other chat channels and forums related to the project.

Sponsor a Project!

- Financial support helps promote continued work and improvements.
- Sponsorship "Tiers" are available directly from the GitHub UI.

Things to Watch For:

- Does it have a license?
- Are issues and PR discussions active, and are the maintainers involved?
- Are labels attached to work items, especially ones to attract newcomers?
- Is there a code of conduct?
- Are there guidelines to contributing?

Lacking any (or all) of the above might be the sign of an abandoned project.

### Communicate Intent

Existing work items:

- Start with the Issue Tracker.
- Look at the Assignees section. Nobody assigned? Possibly available to work on!
- Look for linked Pull Requests, which means the Issue is already being worked on.
- Post a comment on the Issue to indicate interest in contributing. This opens the door to conversation, collaboration, and makes the Issue active (instead of potentially dormant).

New work items:

- Open a new Issue before working on something that is _not already in the Issue list_.
- If it is a new feature, get in touch with the Maintainers directly before starting work. If they are not going to accept the new feature, there is no need to work on it.

Creating A Pull Request:

- Fork the project first.
- The PR will be diff'ed against the origin Repo's working or main branch (see Contributing.md) but the details of the PR etc will be available in your GitHub profile.
- Add a Title and Description for the changes.
- Address the Issue that triggered the need for this PR by prefixing `#` to the Issue number.
- Add any additional helpful commentary.
- If there are changes to tests, point that out as well.
- Be sure to `synchronize` the Fork prior to completing a PR.

After Submitting a PR:

- Check that the PR passes Status Checks.
- If status checks fail, review the Status Check log and find out if your code needs to be updated or if there is a contributor's agreement or something else that need to happen before the PR Checks will pass.
- Check the PR for Comments by project maintainers. There might be necessary changes before the PR can be approved.
- Be sure to respond to comments on your PR!

### PR Good Practices

Git Commit message should complete this sentence: "If applied, this commit will ..."

PR Description should be succinct description of change in the present tense.

Subject line should be limited to 50 characters or less.

Start with a capital letter and end with a period.

Emojis are and `@mentions` are usually okay (I tend to avoid emojis in other people's repos).

Message body:

- Use present tense.
- Include motivation for the code change.
- Explain the `what` and `why`. The `how` is buring in your code. :smiley:
- Avoid `ablist language` in the PR. See [Describing Interactios With UI](https://learn.microsoft.com/en-us/style-guide/procedures-instructions/describing-interactions-with-ui).

Commits:

- Limit the amount of change in your PR.
- Lots of changed files is difficult to review, and opens up more opportunity for introducing bugs.
- Only include commits that are directly related to the PR subject and purpose.

Consider adding Reviewrs or Assignees if appropriate.

Add labels when CONTRIBUTING has guidance on using them.

Consider `linking` Issues in the sidebar.

Customize your subscription to `notifications` on the thread: Subscribed (once participated), Not Subscribed (only `@mentioned`), or Custom (specified events).

### Your Project Takes Off Now What?

Others might come to depend on portions of your code. This would be a good time to find others to take some of the load and ensure your project stays up to date, secure, and active.

## Resources

The [Microsoft Writing Style Guide](https://learn.microsoft.com/en-us/style-guide/procedures-instructions/).

[Describing Interactios With UI](https://learn.microsoft.com/en-us/style-guide/procedures-instructions/describing-interactions-with-ui).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
