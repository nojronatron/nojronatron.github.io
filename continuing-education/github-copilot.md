# GitHub Copilot

This will be a collection of information collected while attending presentations, events, and etc. The first event was an overview of GitHub Copilot at a basic level. Additional topics go into GH Copilot more deeply, providing demonstration, how-tos, and other information.

## Table of Contents

- [Copilot Study Guide Series 1](#copilot-study-guide-series-1)
- [GitHub Copilot Basics - MSFT Reactor](#github-copilot-basics---msft-reactor)
- [Codespaces](#codespaces)
- [Copilot](#copilot)
- [The GitHub Next Team and Project](#the-github-next-team-and-project)
- [Pragmatic Techniques To Get The Most Out Of GitHub Copilot](#pragmatic-techniques-to-get-the-most-out-of-github-copilot)
- [MS Dev Labs Adventures with GitHub Copilot in VSCode](#ms-dev-labs-adventures-with-github-copilot-in-vscode)
- [GitHub Copilot and Infrastructure As Code](#github-copilot-and-infrastructure-as-code)
- [Building Automation With GitHub](#building-automation-with-github)
- [References](#references)
- [Footer](#footer)

## Copilot Study Guide Series 1

Presenter: Ari LiVigni, Sr. Cloud Solutions Architect, GitHub

GitHub Copilot Plans and Features

Online Refs: <https://aka.ms/S-1370>

### Subscription Plans

- Individual, Business, and Enterprise.
- There are many copilots, and all of them are available at the Individual level.
- Business and Enterprise enable excluding files, managing policies, audit logs, increased model rate limits.
- Enterprise also inludes: Copilot knowledge bases and fine tuning a custom LLM.

### Features

- Code Completion
- Chat
- CLI
- PR Summaries
- Text completion (preview)
- Copilot extenions
- Models
- Knowledge bases (Enterprise only)

### IDE Features

- VSCode, JetBrains, and XCode have Copilot integrations/extensions.
- Chat: Copilot icon on bottom of VSCode or near the Command Palette at the top.
- Regular updates.
- Separate Chat Window or In-line Chat within code window.
- Multi-edit and File Editing options: New as of GH Universe 2024. Icons near Command Palette in VSCode.

### Copilot Capabilities Within the IDE

- `Tab` can accept suggestions, `esc` would cancel a suggestion.
- Add a file as context.
- Select a specific model by using the drop-down inside the 'Ask Copilot' window.
  - Chat Inline uses GPT 3.5 Turbo as default, but that could change _and_ other models can be selected (e.g. Claude).
- Generate unit tests using Copilot Chat.
- Insert Into: Terminal, code window, (etc) depending on context such as Commands could be pushed to Terminal, but code blocks would be inserted into the code window.

### Chat Participants

AI Domain experts that can answer questions:

- Prefixed with `@` symbol.
- Domain Experts can accept Slash Commands and Chat Variables!
- `@workspace`: Context without the code within your workspace.
- `@vscode`: VS Code API and the VS Code IDE itself.
- `@terminal`: Knowledge of the terminal content or capabilities.
- `@azure`: Azure-specific knowledge and responses.
- `@github`: Anything GitHub including Issues, PRs,

Slash Commands:

- Prefixed with `/` slash character.
- `/clear`: Start a new chat session, removing prior context (prompts and results).
- `/help`:
- `/explain`:
- `/fix`:
- ...more

Chat Variables:

- Prefixed with `#` hashmark symbol.
- `#selection`:
- `#codebase`:
- `#editor`:
- `#terminalLastCommand`:
- `#terminalSelection`:
- `#file`:

### Copilot CLI

- Must be installed on local VSCode (Codespaces might already have it installed).
- Provides suggestions to prompts within the Terminal.
- Will carry-on a Q&A style interaction within the Terminal.

### Copilot Features in GitHub.com

- Summarize Pull Request Comments w/ "Pull Request Summary".
- Reviewers now contains "Copilot" as of November 2024.
- Index Repositories (uses "Blackbird Search" on the back-end).
- Indexing configuration includes adding repositories and applying filters (using glob-patterns) to the Index feature.
- If there are multiple repos across a group, they can be made "related" by using Github Copilot Knowledge Base.

### Marketplace Features

- Copilot Extensions: Third-party extensions. Extensions can be installed "to a GitHub Organization".
- Models: OpenAI, Phi, etc. There is a playground available to try before adding (or swapping-out) a model.

### GitHub Knowledge Bases

- Organziations can create these.
- Brings together MD documentation across one or more repositories.
- Select one or a number of repositories to include in the "knowledge base".
- Becomes the context for Copilot Chat in GitHub, Visual Studio, or VS Code.
- Select the Knowledge Base within Copilot Chat to set it as the context.
- Can be updated or deleted.
- Can be indexed, to improve Copilot Responses to prompts made against a Knowledge Base (included repositories).
- Indexing is limited per your plan except Enterprise, which is unlimited (Individual: 5; Business: 50).
- Requires an _Enterprise Subscription_.

- [x] Learn more about [GitHub Knowledgebases](https://docs.github.com/en/enterprise-cloud@latest/copilot/customizing-copilot/managing-copilot-knowledge-bases)

## GitHub Copilot Basics - MSFT Reactor

Presenter: Liam Champton @liamchampton

Presenter: Kory - Cloud Advocate @koreyspace

GitHub Copilot is an AI-powered utility that can help you code, debug, and refactor your solutions.

Note: GitHub and Microsoft are working to develop "Co-Pilots" for many scenarios, other than coding.

## Codespaces

- Fully configured dev environment
- Cloud-hosted VM on Linux hardware running a container
- Code editor within a VM, fully desktop-shared
- Leverages Docker Containers
- Clone, Code, Run, and Test all within the Cloud Space
- Displays as a VSCode UI within a browser

### Launch And Use Codespaces

In GitHub:

1. Click Code button
2. Select Codespaces
3. Create new

Plans:

- Free
- Costs by core count and storage

There was also mention of the time-limited constraint of 120 hours per month.

### Dotfiles

Environment variable files like `.env`

### Templates in Codespaces

Quickstart templates designed to get up-and-running quickly:

- React
- Blank
- Jupyter Notebook
- NextJS
- Many more
- Create your own [Custom templates](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)

Templates are OSS and there is an _open invitation to contribute_!

### Benefits

- Reduced time to setup an environment.
- Access to your workspace from anywhere with internet access.
- Setup, Develop, and Debug, all within one Codespaces "window".

### About Frameworks

- It can take time to install a framework onto your Project.
- Possible unknown or unexpected issues with old or unused code, un-optimized code, etc.

Codespaces reduces setup and installation time.

Codespaces also helps with framework setup because n+1 workspaces are just clones of the initial setup!

### Cloud Development Challenges

- Must have internet.
- Must monitor expense.
- Configuration and Setup time (however this is reduced compared to setup on individual hardware/VMs).
- Constraints enable constraining machine types, port visibility (public or otherwise), max idle timeouts, and retention periods.

Configure and name the policy and apply it to Codespaces projects to:

- Reduce probability of of charges.
- Reduce network threat surface.

### Codespaces Environment Benefits

- Promotes accessibility.
- Scalable across teams.
- Customizable.
- (something else).
- 60 hours free!

Configurable, customized environment!

- Codespaces lifecycle starts at create, ends when deleted. Rebuild can be done anytime between Create and Delete.

Since Codespaces uses a virtual machine behind the scenes, code can be built and executed _in the same window_.

Multi-window layouts support viewing multiple files within the environment window e.g.: Explorer, README.md, some-file.js, and a Terminal window.

Can open a repository using other IDEs:

- VSCode.
- IntelliJ.
- Others.
- GitHub Desktop.
- Visual Studio.

### Processes That Kick-Off When Creating New

1. VM and storage are assigned to new Codespace.
2. Container is created.
3. Connection to Codespace is made.
4. Post-creation setup is made.

Components:

- Container.json: variables, extensions, and more.
- Dockerfile: Defin env and dependencies to execute it.
- docker-compose.yml: Execute multipel containers.

### Compare With GitHub.dev

Differences from Codespaces:

- Free, completely.
- Available for any GitHub user.
- Startup: Use right away without installation with just a keypress.
- Compute: No compute, cannot build and run or use Integrated Terminal.
- Terminal Access: None
- Extensions: Only subset of extensions can run (web-run only).

### Codespaces Resources

As of March 2024: Prepare for [GitHub Certification Exams](https://aka.ms/github-certification).

[intro-codespaces repository](https://github.com/gittogethers/intro-codespaces).

[Self-guided Codespaces walkthroughs](https://github.com/skills/code-with-codespaces).

## Copilot

- Write, Test, Explain code, and get answers.
- There is a free-trial link to get started.
- Supported in Visual Studio, Neovim, VS Code, and JetBrains IDEs.

Copilot Chat:

- Instead of asking an LLM to generate code, then copy-paste into an IDE.
- Integrated into VS Code to collapse workflow to fewer steps.
- Uses an LLM that is tuned toward software coding (whereas ChatGPT versions are more widely scoped and generic).
- Relatively language-agnostic (JS, Rust, C#, Python, C++, etc).

Demo Notes:

- Starting CodeSpaces for a repo takes about 20-30 seconds from setup to code-ready.
- `.devcontainer/devconatiner.json`: Not required, but good for smaller images, points to code language image, and customizations e.g. Extensions.
- DevContainer config will also allow running scripts e.g. bash script that runs `npm install`.
- A Universal Image is available that covers many languages in one, but a specific template will be much smaller (and faster to load).
- CodeSpaces allows using Terminal and other VS Code utilities just like when running on local e.g. `npm install` and `npm start` work as expected.
- CodeSpaces allows launching a web browser (NextJS, React, etc) directly from the Dev Environment UI.
- CoPilot might suggest variable names like 'min' that might not always be obvious identifiers.

## The GitHub Next Team and Project

[VSCodeDay](https://learn.microsoft.com/en-us/events/vs-code-day-2023) was an event in April 2023, focused on VS Code and some of the Microsoft and GitHub improvements and integrations. The following notes result from watching some of the VS Code Day 2023 presentations.

### Whats New WIth Github Next

Presenter: Amelia Wattenberger, Principal Research Engineer, GitHub Next

Amelia created VSCode Extension: Footsteps, as a result of an interview challenge (homework) in 2020. This is published in the Marketplace.

Note: VS Code Extensions might be built in TypeScript.

Check out [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension).

#### Summary Notes

CoPilot: AI pair-programmer.

GitHub Next team is a prototyping team "build prototypes, not products".

- Don't know all the use cases.
- Challenged by getting user feedback, so built-in feedback mechanism.

CoPilot started as a set of Panels:

- An Explainer extension. Paste code into a window, ask the prompt to explain the code, view the AI result.
- A Translater extension: Paste one code language into the panel, tell the prompt which code to translate it to, view the AI result. Example: JavaScript -> Python.
- Test Generation extension. Generates tests based on prompts, runs them in the background, and will offer to fix broken tests.

Get familiar with VSCode Primitives to help improve Extension creation process.

GitHub Next is working on LLM-based solutions like:

- Copilot Voice: Voice-operated coding is possible, for improved accessibility!
- Code Brushes: Make coding more tactile, similar to Photoshop brushes that _paint_ or modify your code.

##### VSCode Primitives

Contextual Toolbar: CodeLens as an example. Tools that appear in-line or above a code block or segment.

Line Decoration: Colorization, highlighting, etc of line(s) of code. Usually signals something such as in Footsteps extension, it highlights code you've recently edited.

Diagnostic panel: Problems View as an example. Other tools can be put in the Diagnostic Panel, usually related to logging, errors, results from actions, etc.

Webview Panel: The list of tools like Explorer, Extensions like ThunderClient or Azure, the Extensions add/remove tool, Profile/Login status icon, and the Settings icon.

## Pragmatic Techniques To Get The Most Out Of GitHub Copilot

### Presenters

Allison Weins: Senior Product Manager, GitHub

Burke Holland: Principal Cloud Advocate, Microsoft

### Limitations

- Training data: More data is better but it is not always available (COBOL vs JavaScript). Also, not all code is _good_ code, such as abandond repositories.
- Copilot is not a compiler: There is no guarantee that the code will compile or run. Use your experience and existing in-IDE tools to ensure the code is buildable and runnable.
- AI cannot read your mind (just like a pair programming human).

### Single, Specific, Short

- Single: Focus on performing one thing at a time.
- Specific: Be specific with your input. Use very specific plain language.
- Short: Expect a short answer in response.

### Examples via Demos

- Write a comment that follows the 3S's rule, above.
- Sometimes a 'nudge' is needed to get Copilot started. For example, after your
- Write: `function removeHTMLCharsFromStr(str) {}` and Copilot might write the entire function if it is just a line or two.
- Copilot excels at patterns and "stuff you've forgotten".
- Press `ALT + Slash` to open Copilot _inline chat_.
- "Trust but Verify": Ask Copilot what a code block or line of code does - then use VS Code extensions and tools to validate the code.
- Copilot Chat will include necessary imports in addition to actual code, whereas VS Code features like IntelliSense will not.

### Provide Effective Intents

- Craft effective prompts within code comments.
- Iterate your prompts to get better results.
- Sometimes it is better to remove existing (previously generated) code and allow the iterated prmopt processing.

### Relevent Inputs and Context

- Copilot will use other open windows to help it find a possible solution.
- Copilot can be allowed to continue writing line-by-line, or you can stop it and provide a new prompt.
- Copilot does _not_ look at your entire project.
- Copilot _will_ look at other open files in your editor during your session.
- Copilot _will_ look at the code at and around your cursor.

_Remember_: Prompts are limited, so as not to overwhelm the network, or the cloud-based processing.

### Highlight Suggestions

1. Highlight code and the suggestions lightbulb will appear.
1. Click the lightbulb and Copilot will provide suggestions for the highlighted code.
1. You have the option to accept or reject the suggestion.

## MS Dev Labs Adventures with GitHub Copilot in VSCode

These are notes from a livestream hosted by
Olivia Guzzardo
Marc Baiza Tech Progm MSFT AI + ML
Abril DevTools at MSFT

### Copilot Adventures

[Repo](https://aka.ms/CopilotAdventures) set up with challenges to solve using GitHub Copilot.

There are beginner, intermediate, and advanced level challenges.

### CoPilot Chat

Press `CTRL + i` to launch CoPilot Chat in VSCode or CodeSpaces.

Plaintext inputs:

- Be specific. If you want Python code, then identify that.
- Be clear. If you are looking for a doubly-linked list then you'll want to specify that condition.

Slash Commands:

- Shortcuts to common CoPilot Chat inputs.
- `/doc`: CoPilot writes a code comment for existing adjacent code.

How can GH CoPilot help me?

- Explain how existing code works.
- Write code for you.
- Write unit tests.
- Find errors in code.
- Ask it how to make existing code more maintainable and readable.

## GitHub Copilot and Infrastructure As Code

Presentation: How to Accelerate Infrastructure As Code Adoption - MSFT Reactor

Presenter: Adil Touati - Sr. Cloud Solution Architect, Montreal CA. [GitHub](github.com/Adeelku)

### About GitHub Copilot

Copilot and Copilot Chat:

- VSCode and Visual Studio Extensions.
- Individual, Business, and Enterprise licensing schemes (free-trial options are available too).
- AI "pair programmer".
- Offers in-line actions.
- Chat adds a chat-bot interface.
- Accuracy is not always 100%.
- Prompting is important. Supplying enough information and context will help drive more correct answers.

Advice:

- Always test output for suitability and correctness.
- Learn from Copilot! It can provide example code that you might not be familiar with, and Copilot can explain in detail.
- Leverage existing solutions to speed development.
- Generate large codeblocks quickly!

### Copilot For IaC - In Action

Use prompt-engineering concepts.

Use `#<filename>` to reference all related files when prompting Copilot. Lots of files can be referenced.

Highlight code, press `CTRL` + `I` and the Inline Prompt will automatically use the highlighted code as part of the question context.

## Building Automation With GitHub

Microsoft Reactor session notes from "Building Automation With GitHub"

Presenters:

- Alfredo Deza, Developer Advocate
- Abril Urena, Developer Advocate

This session is part of preparation for GitHub Cloud Certification.

There will be more sessions June 12th, 19th, and 26th.

Some notes:

- Whenever working with a new repository, review the README, the folder structure, and take a peek at some of the code files to get familiar with the code language and style.
- Use a Linter to check code. `Flake8` was mentioned as an effective Python linter.
- python.defaultInterpreterPath: Points to the vscode venv that the Python project will run in.
- Ask Copilot to assist creating a GitHub Action to do things like 'linting'.

## References

[General Links](https://aka.ms/levelup-links) from 'Level Up Your App Development Using GitHub Copilot and Codespaces' MSFT Reactor Session.

Check out [GitHub Next](https://githubnext.com) for information on what the GitHub Next team is working on.

Developing [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension).

GitHub CLI supports Github Copilot! See [Github Copilot CLI Installer](https://github.com/cli/cli).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
