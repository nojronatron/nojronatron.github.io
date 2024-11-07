# GitHub Copilot

This will be a collection of information collected while attending presentations, events, and etc. The first event was an overview of GitHub Copilot at a basic level. Additional topics go into GH Copilot more deeply, providing demonstration, how-tos, and other information.

## Table of Contents

- [Copilot Study Guide Series 1](#copilot-study-guide-series-1)
- [GitHub Copilot Basics - MSFT Reactor](#github-copilot-basics---msft-reactor)
- [Codespaces](#codespaces)
- [What Can Copilot Do](#what-can-copilot-do)
- [The GitHub Next Team and Project](#the-github-next-team-and-project)
- [Pragmatic Techniques To Get The Most Out Of GitHub Copilot](#pragmatic-techniques-to-get-the-most-out-of-github-copilot)
- [MS Dev Labs Adventures with GitHub Copilot in VSCode](#ms-dev-labs-adventures-with-github-copilot-in-vscode)
- [GitHub Copilot and Infrastructure As Code](#github-copilot-and-infrastructure-as-code)
- [Building Automation With GitHub](#building-automation-with-github)
- [Responsible AI with GitHub Copilot](#responsible-ai-with-github-copilot)
- [Advanced GitHub Copilot Features](#advanced-github-copilot-features)
- [IDE, Chat, and Command Line Techniques](#ide-chat-and-command-line-techniques)
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
- `@workspace`: Context without the code within your workspace. Can also generate an entirely new project.
- `@vscode`: VS Code API and the VS Code IDE itself. For example, how to change settings in VS Code.
- `@terminal`: Knowledge of the terminal content or capabilities. Can do things like GCI the local file system.
- `@azure`: Azure-specific knowledge and responses.
- `@github`: Anything GitHub including Issues, PRs,

Slash Commands:

- Prefixed with `/` slash character.
- `/clear`: Start a new chat session, removing prior context (prompts and results).
- `/help`:
- `/fix`:
- `/explain`: Describe the selected code line, block, or file.
- `/fix`: Proposes solutions to problems in selected code.
- `/generate`: Given a set of requirements, will generate code, creating functions or other code blocks.
- `/optimize`: Analyzes selected code and suggests improvements to runtime efficiency.
- `/tests`: Create unit tests for teh selected code. Tell Copilot which unittest framework to use and it will generate code for you.

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

## What Can Copilot Do

- Write, Test, Explain code, and get answers to questions.
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

### Summary Notes

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

### VSCode Primitives

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

These are notes from a livestream hosted by:

- Olivia Guzzardo
- Marc Baiza Tech Progm MSFT AI + ML
- Abril, DevTools at MSFT

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

## Responsible AI with GitHub Copilot

Goals:

- [x] What are the principles of responsible AI usage?
- [x] What limitations are associated with AI, and how to mitigate risks.
- [x] What are best practices to ensure generated code meets ethical and project standards.
- [x] How transparency and accountability in AI systems is necessary.

### Responsible AI And Governance

Risks of AI:

- Sometimes makes difficult to interpret decisions.
- Lack of transparency, accountability.
- Unintended (and harmful) outcomes.
- Biased decisions, privacy violations.

Governance Over AI:

- Develop, asses, and deploy safely, in trusted and ethical way.
- Ensure decisions are equitable and beneficial.
- People and their goals should be focus of design.
- Fairness, reliability, and transparency are key tenents.

MSFT and GitHub's Six Principles of Responsible AI:

- Fairness: Treat people fairly through trained-data review, model testing using demographic samples, use of adversarial biasing, model performance monitoring, controls to override unfair model scores.
- Reliability and safety: Consistent, trustworthy operation, with safe responses to unexpected inputs, and resist harmful manipulation. Minimize unintended harm. Robust, accurate, predictable behavior under normal conditions.
- Privacy and security: Protect user privacy and data security through obtaining user permissions before collecting data, use only the data necessary to complete the job and check data points to ensure only necessary data is included, and anonymizing personal data. Encryption, secure vaults, HSMs (hardware security modules), and key management are used and managed.
- Inclusiveness: Empower _everyone_ equally, and disadvantage no one. Include accessible controls for all abilities. Worldwide availability, without excluding any geographies. Input into the system by anyone is allowed.
- Transparency: Use validation framework to describe operation, justify _design choices_ behind the AI system, be honest about capabilities and limitations of AI system, and enable auditing with logging and reporting capabilities.
- Accountability: AI Creators should be responsible for how their AI systems operate. Use constant monitoring, and enable detecting, managing, and mitigating risk. "AI systems must be accountable to people, and companies deploying AI systems must take responsibility for [their AI systems] operation." _[Microsoft Learn documentation]_

### Key Takeaways

1. Ensure AI systems are safe, trustworthy, and ethical.
1. Create AI systems that are easy to understand.
1. Ensure AI systems perform equally well across all demographic groups.
1. Address potential biases by reviewing training data, test with balanced samples, and use _adversarial debiasing_ techniques.
1. Ensure AI systems are transparent, with easy to understand AI processing and decisions.
1. Ensure generated code aligns with project-specific conventions and requirements.
1. Fairness, Inclusiveness, Accountability.

## Advanced GitHub Copilot Features

- [x] Use slash commands to make code changes using `[ctrl] + i` and a prompt such as 'describe this code block'.
- [x] Use GitHub Chat feature to interact, prompting Copilot to write unit tests, for example.
- [x] Ask questions about a project using an agent such as `@workspace`.

List of Advanced Features:

- Ghost Text: Suggestions provided by Copilot while typing in an IDE with Copilot enabled. Use `[tab]` key to accept it, or just ignore it to decline. Open-files are automatically used as context.
- Copilot Chat: Interactive discussion feature. Click the chat icon in the IDE, then start asking questions about code being worked on, or other software-related questions.
- Inline Chat: Interact with Copilot without opening a new window. `[ctrl/Command]` + `[i]`. Reduces developer context-switching to interact with Copilot.
- Slash Commands: Specify an _intent_ to prefix a prompt. `/` prefix a command like `tests` or `docs` or `fix` or `describe`. Minimizes prompt writing and maximizes generated output relatability.
- Agents: Ask questions using a specific context such as `@terminal` or `@workspace`. Prefix an Agent target with `@` symbol, then type the question/prompt for a context-aware response.

_Note_: `\fix` et al are known as _implicit prompts_.

_Note_: `@workspace` uses _open files_ in the editor as additional context.

## IDE, Chat, and Command Line Techniques

- [x] Use auto-suggestions.
- [x] Use multiple suggestions pane.
- [x] Provide content to Copilot via inline commands, block comments, and doc strings.
- [x] Interact with Copilot through natural language conversations.
- [x] Generate complex code, and debug issues through natural language.
- [x] Obtain code explanations in real-time.
- [x] Improve relevance of Copilot Chat suggestions through scope referencing, slash commands, and agents.
- [x] Set up and use GitHub CLI for: Command explanations, suggestions, and to execute commands.

### Completion Supported languages

Currently fully supported:

- python
- JavaScript
- TypeScript
- ruby
- go
- C#
- C++

Copilot will understand and could help with most other languages and frameworks - the above are the supported ones.

### Suggestions

- Auto Suggestions: Ghost code is displayed in-line, suggesting possible code additions.
- Multiple Suggestions Pane: Hover over Ghost Code to see additional commands like Accept, Accept Word, or to see additional suggestions.
- Method recognition: Start typing a function or method and Copilot will ghost-write a suggestion for an entire implementation, following your code style.
- Convention Mimicing: Copilot will mimic existing code style, variable and method naming conventions, formatting, and design patterns.
- Comments Trigger Suggestions: Natural Language Processing and Contextual Analysis are used to convert code comments into suggestions. Leverages in-line, block, docstring, TODO, and API documentation styles.

### Copilot Chat

- Interactive, conversational AI assistant, available directly in the IDE.
- Support natural language processing.
- Understand context of a selection, file or files, or an entire project.
- Better-suited for generating complex code or boilerplate code for specific design patterns.
- Good for generating complex regular expressions or developing advanced data structures.
- Analyzes errors in code and suggests potential fixes with step-by-step explanations.
- Explain code within complex code snippets, and offer insights into best practices and potential optimizations.
- Also has a `Feedback` feature so the user can rate suggestions.

### Copilot Chat for Command Line

Offers intelligent suggestions and simplifying tasks:

- Streamline command-line workflows.
- Provide explanations for unfamiliar commands.
- Suggest commands based on needs/current activities.
- Execute commands on your behalf.

Common Commands include:

- 'ghcs explain': Follow the command with a quoted string of the command that Copilot should explain.
- 'ghcs suggest': Follow with quoted string containing a question or prompt for Copilot to generate a response to.
- 'ghcs revise command': Ask Copilot to generate a new suggestion based on the last prompt.
- `ghcopilot config`: Enable configuring Copilot CLI.

Alias Configuratin:

- Allows executing commands on your behalf.
- Can be configured in PowerShell, Bash/*sh, and mac Terminal.

Organizational Settings:

- Policy may disable or enable other features and capabilities of the CLI.

Data Handling:

- Prompts are _not retained_ by Copilot.
- Analytics metadata _is retained_.
- Use `gh copilot config` and select from the on-screen list of options.

### Improving Copilot Chat Responses

- Scope Referencing: Use File References, environment references (e.g. `@workspace`), Slash Commands (e.g. `\describe`)

## Management and Customization with Copilot

- [x] Understand plans, management, and customization features.
- [x] Understand contractual protections and siabling matching public code.
- [x] Manage content exclusions.
- [x] Common issues with Copilots and their solutions.

### Copilot Policy and Customization Features

Individual, Business, and Enterprise license Copilot has varying Managemetn and Customization features.

Management Policies:

- Individual: Enable public code filter.
- Business: Public code filter, User management, data exclusion from training, enterprise grade security, IP indemnity, SMAL SSO Auth, and Usage metrics.
- Enterprise: All Individual and Business policies plus Require GitHub Enterprise Cloud.

Customization Features:

- Individual: Unlimited integration with Copilot Extensions (currently in beta), Build private extension for internal tooling (currently in beta).
- Business: Same as Individual.
- Enterprise: All individual and Bueisness features plus Tailed chat conversations to private codebases, attach organization's knowledge bases to chat, and fine-tuned models for code completion (coming soon as an add-on).

Consider these factors when deciding on a plan for your organization:

- Data privacy and security.
- Policy management at the organizational level.
- Data collection and retention.
- IP Indemnity and Data Privacy (legal).

Safeguarding Code and Data:

- IP Indemnity: Set 'matching public code: blocked' to enable indemnity and GitHub assumes legal responsibility for IP claims.
- Data protection Agreements: Offered by GitHub, provides secure, responsible data handling with transparency.
- GitHub Copilot Trust Center: Detailed information about how Copilot works, security measures, IP safeguards, etc.

### Matching Public Code Feature

1. Go to the Organization's GitHub page.
1. Open the profile.
1. Click Enterprise Settings (or Organizational Settings).
1. Click Copilot.
1. Select 'Suggestions' drop-down.
1. Select 'Matching Public Code'
1. Click 'block'.
1. Click Save.

### Content Exclusions

Can be set at the Repository level (go to Repository Settings), or the Organizational level (load the Organization page and open Settings).

Impacts of exclusing public code:

- Limits the codebase upon which Copilot acquires fodder for its suggestions.
- Could reduce overall context available to Copilot.
- Could limit accuracy and usefulness of suggestions.

Balance security and functionality when excluding content:

- Code Completions are disabled on excluded files.
- Suggestions will no longer draw from excluded files, limiting context scope.

### Troublshoot Common Copilot Issues

Missing Code Suggestions:

- Check internet connection.
- Update Copilot Extension.
- Verify IDE compatibility.
- Review Content Exclusions to see if files are excluded.

Content Exclusion Issues:

- Application of exclusions is delayed by up to 30 minutes.
- Reload the exclusions in the IDE to confirm application is set.
- Verify affected user is a member of the Organziation with the Content Exclusion settings applied.
- Content Exclusion application can be seen when an affected file is loaded and a slash `/` appears over the Copilot icon, indicating the file is excluded.
- Some IDEs do not support Content Exclusions in Copilot Chat - check the IDE and Copilot documentation to confirm expected behavior.

Triggering Copilot Suggestions:

- Provide clear context to Copilot.
- Use meaningful variable and method/function names.
- Use a specific Copilot command to generate a better response, such as use Chat instead of In-line, or using a Domain Expert `@`, Slash Command `/`, or Chat Variable `#`.
- Adjust prompt length. Too short or too long of a prompt might not provide enough context to generate a valuable response.

## Streamline Dev Productivity With Copilot

- [x] ID specific ways to integrate Copilot into dev workflows.
- [x] Understand where Copilot can positively impact the SDLC, as well as its limitations.
- [x] Measure Copilot impact on development performance.

### Boost Dev Productivity

Key areas where Copilot can help with developer productivity:

- Code Suggestions: Snippets that illustrate usage of unfamiliar functions, or provide guidance.
- Language Support: Wide number of languages are highly supported, others can be used but require additional care and monitoring.
- Documentation: Reduce the need to constantly refer to external documentation to implement code.

Minimize Context Switching, and avoid disrupting workflow and reduced focus:

- In-editor assistance: Suggestions directly in IDE.
- Quick references: Get rapid, accurate method call and parameter suggestions without having to consult documentation.
- Code completion: Code auto-completion of boilerplate code speeds up implementation, reducing train-of-thought interruption.

Enhance documentation writing:

- In-line commands generate contextually relevant comments even for complex code segments.
- Function description: Developer doesn't have to stop and create wording to document code.
- README generation: Automate creation of useful README by providing structure and content resources that Copilot will generate from.
- Documentation consistency: Maintain consistent style across a project.

Automate 'boring' work:

- Boilerplate and common functionality code generation.
- Sample data creation.
- Writing unit tests.
- Translate code and refactor code quickly and easily.

Personalized code completion:

- Most accurate, relevant code completions are created from the current dev environment context.
- Copilot learns coding patterns, preferences, and tailors suggestions accordingly.

### Align with Developer Preferences

Code Generation and completion:

- Multiple suggestions for ambiguous scenarios.
- Language-specific idioms: Suggests language-specific code and best practices.

Unit Tests and Documentation:

- Generate relevant test cases.
- Stub-out documentation for functions, classes, modules, etc.
- Copilot expands comments into suggestions and code generation.

Refactoring:

- Pattern recognition, for better suggestions of alternative, more efficient code.
- Syntax suggestions based in modern coding languages and frameworks.
- Consistency of refactoring code: Across a project Copilot will maintain existing code style.

Debugging Assistance:

- Explanation of errors.
- Generation of log statements.
- Suggestions for test cases.

Data Science Support:

- Statistical function code generation.
- Data visualization code suggestions.
- Data preprocessing task suggestions such as scaling numerical features, encoding categorical variables, etc.
- Model evaluation metrics and visualizations.

### Remember SDLC?

Requirements Analysis:

- Rapid prototyping.
- User story implementation.
- API Design.

Design and Development:

- Boilerplate code generation.
- Design pattern implementation.
- Code optimization.
- Cross-language translation.

Testing and QA:

- Unit test creation.
- Test data generation.
- Edge-case identification and coverage.
- Assertion suggestions for multiple unit testing frameworks and code languages.

Deployment:

- Configuration file generation.
- Deployment script assistance.
- Documentation updatees.

Maintenance and Support:

- Bug-fix Suggestions.
- Code refactoring.
- Documentation updates.
- Legacy code understanding.

### Copilot Limitations in SDLC

Code quality and correctness:

- Potential for errors, not meeting requirements.
- Security concerns with generated code, not necessarily meeting best practices.
- Context misinterpretation causing inappropriate suggestions.

Language and framework specificity:

- Varying performance between languages and frameworks (better suggestions in some than others).
- Niche terminologies: Newer languages and frameworks' syntax might not be included in context or generated output.

Dependency on training data:

- Bias in suggestions. Includes possible outdated coding practices.
- Copyright concerns (an ongoing debate).

Complex problem solving:

- Limitations in high-level deisgn: Does not always grasp complex architectural decisions.
- Creativity constraints: Copilot cannot replace human creativity in solving novel problems.

### Measuring Productivity Gains

Use the REST API for GitHub Copilot usage metrics!

- Endpoints such as `GET /enterprises/{enterprise}/GitHub Copilot/usage` provide breakdowns of aggregate usage metrics.
- WRRC REST response codes supported.
- JSON body object with response data.

Code example _[Learn.Microsoft.com]_:

```text
curl -L -H "Accept: application/vnd.github+json" -H "Authorization: Bearer {TOKEN}" https://api.github.com/enterprises/{ENTERPRISE}/GitHub Copilot/usage
```

Implement a measurement framework:

1. Evaluate: Review leading indicators like developer satisfaction and task completion rates. Collect average daily usage and total acceptance rate statisics.
1. Adopt: Monitor productivity metrics and 'enablement indicators'. Areas where usage training is necessary will become apparent.
1. Optimization: Use REST API usage metrics to fine-tune Copilot impact.
1. Sustained Effeciency: Continually evaluate effectiveness using ongoing API monitoring.

Github Copilot Developer Survey advice:

- Use Short-form and/or Long-form depending on your organizational requirements and goals.
- Structure the survey to focus on _either_ immediate feedback or deeper analysis such as long-term benefits.
- Consider privacy concerns of users taking the survey.
- Use BI tools to perform data tracking and reporting, statistical analysis.
- Use the insights to develop training and go-forward plans for continual improvement across teams and the organization.

## Developing Unit Tests Using Copilot

- [x] Create tests using Copilot extensions.
- [x] Target edge cases in unit tests using Copilot.
- [x] Exercise using Copilot to test a project to verify unit tests run successfully.

### Copilot Tools is VS Code

Five different ways to interact with Copilot:

- Code line completions (aka ghost code).
- Inline chat. Chat within the editor, in-line with the code.
- Chat view. The Copilot Chat window.
- Quick chat. Ask a question, get a generated response, get back to work.
- Smart action. Copilot will perform actions without you having to write a prompt.

Support for Unit Tests using C#:

- .NET 8.0 SDK.
- C# Dev Kit Extensions (contains other extensions as a single installation).
- A test framework package added to the project like xUnit, NUnit, or MSTest.

### Enable a Test Framework in VS Code

1. Create a project (or solution or projects) that has a UnitTest project (use `dotnet new xunit ...` for example).
1. Open Command Palette.
1. Select `DotNet: Generate Assets for Build and Debug`.

### Develop Tests Using Copilot

Open the code file that contains code that will be tested and Copilot will help with these tasks:

- Write unit tests in the installed framework for code under test open in a tab.
- ID and write test cases for edge cases and boundary conditions (e.g. error handling, null values, and unexpected inputs).
- Suggest assertions to ensure correct function operation validation.

Try the following tactics to have Copilot write tests:

- Open a code file and display just a single method in the code editor, then open Copilot Chat and request `Write unit tests for the method in the #editor`.
- Open a code file and select the method that should be tested, open Copilot Chat and request `#selection write unit tests for this code`.

### Run and Manage Test in VS Code

Run, debug test cases, view test results, and manage test cases using Test Explorer:

- Within the code: C# Dev Kit will generate a green arrow indicating a unit test can be executed right there in the code.
- Test Explorer lists all discovered cases, their last-run result (pass, fail, not run), and has start, stop, and other tools.
- View Test Results via editor decorations or from within Test Explorer.
- Use the Command Palette to call commands like `run all tests`, like you would using `dotnet` command in the terminal.
- VS Code Test Settings are available within the VS Code Settings editor.

## References

[General Links](https://aka.ms/levelup-links) from 'Level Up Your App Development Using GitHub Copilot and Codespaces' MSFT Reactor Session.

Check out [GitHub Next](https://githubnext.com) for information on what the GitHub Next team is working on.

Developing [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension).

GitHub CLI supports Github Copilot! See [Github Copilot CLI Installer](https://github.com/cli/cli).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
