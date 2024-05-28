# Open Source Learnings and Activities

## Table of Contents

- [Index of Plans and Open Source Contributions](#index-of-plans-and-open-source-contributions)
- [Building An Open Source Program Using GitHub Best Practices](#building-an-open-source-program-using-github-best-practices)
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

### How To Do This?

Initial Questions to Get Started:

- Are there other data that go with the project but are not Code? Bugs in a separate logging system? Plans and architectural documents that need to be included with the OSS repo?
- Are there binary files/artifacts that will need to be stored in an [Git LFS](https://git-lfs.github.com/) or other non-Git storage medium, like spreadsheets, build outputs, or presentations?
- What items need to be in the `.gitignore` file to help enforce version-control policies?
- Are the communications and instructional files ready e.g. README, LICENSE, CONTRIBUTING, and perahps a SECURITY markdown?
- Are there other `.gitattributes` that need to be configured to ensure proper git configuration of LF/CRLF handling? *[Nojronatron]*
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

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
