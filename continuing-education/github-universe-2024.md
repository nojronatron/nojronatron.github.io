# Github Universe 2024

Randome notes taken while virtually attending GHU'24.

"The world's fair of software"

## Keynote Tuesday 29-Oct-2024

Presenter: Thomas Domke

- This is the 10th anniversary GHU.
- Python has surpassed JS as the most-used language stored in GitHub repositories, driven mainly by ML and AI.
- Copilot pillars: AI-infused, conversational coding, and multi-model functionality.
- Next-gen Copilot: AI-native (core and cannot be separated from the dev experience), AI Agents (execute tasks at your direction via various Agents), and Multi-model choice (many models are available, with many key purposes, which are now used in the Copilot AI backend).
- All GH Copilot+ users now have access to OpenAI-preview.
- Clause 3.5 Sonnet (Anthropic) is now integrated into Copilot.
- Google Gemini 1.5 models will be available in Copilot now.
- Github Spark: AI-native tool to build Apps using Natural Language.
- Natural language capabilities have extended beyond English, and a few other languages, to enable global language intepretation and interaction with Github Copilot and it's system of tools and features.

Jared Caplan, AI Scientist, co-founder of Anthropic:

- Anthropic expected AI would progress rapidly, with the goal of putting AI models into OSS developer hands rapidly.
- Claude roadmap: Model complexity made available via "agentic" (agent-based) services, for many uses outside of just the Terminal or Chat window (coding, testing, other application integrations).

Cassidy (the video stream broke so details will be filled in later):

- Multi-lingual capabilities of Github Copilot.
- GH Copilot workflow: Repo indexing, Intent detection, and Workspace analysis.
- Multi-file editing now available in GH Copilot.
- GH Copilot Custom Instructions: 'copilot-instructions.md' guides GH Copilot how to build certain functions (and more).
- GitHub Copilot for VS Code includes these features plus code-review and code-indexing, as of _this week_.
- More GH Copilot Extensions are coming (usually targeting specific IDEs and products), and OSS contributions and Extensions can be built.
- GH Copilot now available in Apple XCode.

Tim Rogers Staff Product Manager, GH Copilot:

- Models! GH Models: Pick a model, experiment with the Model Playground, and then deploy to production.
- GH Model Playground allows exploring a model _or comparing two models side-by-side_.
- GH Model Playground includes a `code` tab to view how the model is executed, including API Key acquisition for deploying the code.
- Multi-modal Models: Can accept images (as well as text).
- All GH Users can _now_ access GH Models including access to the GH Model Playground.

Eirini Kalliamvakou Staff Reseracher, GitHub

- Copilot Workspace Tech Preview was released six months ago.
- Agents: Spec, Plan, and Implementation, all under dev direction, workflow tasks within Copilot Workspace.
- Brainstorm and Build & Repair agents have been added.
- VSCode Extension now available.
- CP Workspace now integrated into GH Pull Requests.

Karan M V, Dir Int'l Developer Releations, GitHub

- Context: Implement a new feature in an active Repository. Fire-up a new Branch in Copilot Workspace, and Brainstorm will open.
- Brainstorm: Describes current behavior, provides some information on how to approach solving the problem, and suggests some questions to ask around solving a problem.
- Plan: This will suggest what changes to make in what files based on the Brainstorming inputs. Edits are suggested (via Diffing) per the usual GH Copilot interaction.
- Revisions can be made during the Plan interactions, supporting _many languages_.
- GH Workspace has Build, Test, and Run command interactions.
- Copilot Workspace is now available in GH Pull Requests.

## Github Spark

- Basic web-form like interface.
- Select a model, input a prompt, or look at recently created "Sparks" (which are previously created projects).
- Iterate over the suggested solution to update operational code.
- Themes and other settings can be edited using the Themes and Settings buttons.
- Also, connection to Data can be managed using another button.
- This is pre-release, not yet publicly available.

## AI Native Developer Experience

- Integrate AI into the full software development lifecycle from design to deploy, including ideation, code-generation, test development, deployment pipelining including production, and ongoing maintenance and improvement collaboration.
- Immutable GitHub Actions Publishing was announced. See [publish immutable action repository](https://github.com/actions/publish-immutable-action) on GitHub.com.

## Github Copilot Can Do That ?

- Use inline chat in a Jupyter Notebook to help write code in a code block. Always check the proposed output and use the in-line input box to refine Copilot's next response.
- Clean tabular data using inline Copilot prompts.
- Create an AI Model using inline chat input. Usually, simple requests will result in valuable results. Sometimes a more specific configuration and code is necessary, so a larger, more specific request (and one or more follow-ups) are required.
- Copilot can read-aloud!
- Copy an error message directly into copilot and use `\fix` to get advice on how to fix it.
- Build-out unittests for a project. Copilot can suggest test framework and explain how to install and configure it. It can also generate tests based on the code file(s) you want tested. Open up files and use `@workspace` to ensure Copilot has the context of the files when generating its response.

## Github, SDLC, and Security

Presenter: Mike Hanley, Github CTO (product, engineering, support, and security):

- Size and scale of GitHub makes security a unique and complex challenge. 518 Repositories today (up 25% from 2023). 1.5B merged PR's, a 32% increase over last 12 months. Average 7.1B API Requests every day.
- "Good security starts with what works for the developer". Don't add security late in the process.
- Software culture should include security as a team sport, not a hidden feature or secret sauce.
- AI can help 'left-shift' security.

Some Tools and Processes to Improve Security Posture (as Github sees and does it):

- Repo Rules, Branch Protection, and Push Protection.
- PR Security Tools: Secret Scanning, Code Scanning, and Dependabot...and now Copilot Autofix!
- GH treats itself as "customer zero".

Things to think about:

1. Good security starts with the developer. Security should not be an after-dev thought.
2. AI is helping to shift security left.
3. Security culture eats security strategy for breakfast. Security is a team spot.

Whitney Imura, Sr Dir Engineering, GitHub:

- Use CodeSpaces.
- Sanitize user code to meet security guidelines.
- Branch Rules ensure critical branches are safeguarged.
- Merge Queues:
- RepoRules: Evolved from Branch Protection Rules. Rulesets are applied to the Organization and Repo level. Security and Compliance Teams can develop these rules for the team/organization. Enforcement Status allows an 'evaluation mode', as well as 'disabled' or 'active', allowing careful management and application of new rules.
- Bypass Ruleset: Users in these rules do _not_ need to be a Repo Admin to override a push. It is possible to report (audit) when the rule is activated.
- Ruleset Recipies: GitHub repository with publicly available RuleSets as recommendations for OSS or Enterprise.

Xavier Rene-Corail, Sr Dir Security Research, Github Security Labs:

- Not all Devs are security experts (of course).
- PRs are the key focus area to detect (and remediate) security risks and vulnerabilities.
- Technical Debt in existing code: Utilize CodeQL Analysis to find security issues right in the repo!
- Copilot Autofix for OSS is now available for free!

Michael Recachins, Staff Engineer, GitHub:

- Fundamentals program: Governs secure, high quality code ships, encouraging collabortive code teams.
- Service Catalog: Visibility into infrastructure health and security. For Engineers and management.
- Use Security Alerts in your repository Settings to view Dependabot and other Alerts.
- Security Campaigns is now in public preview (part of GitHub Security).
- Copilot is integrated into GH such that it makes recommendations for how to fix alert issues directly in the repo, whether in a PR or in some branch.
- Entitlements will be available soon. See [gh.io/entitlements](gh.io/entitlements).

## Resources

## Footer

- Return to [ContEd Index](./conted-index.html)
- Return to [Root README](../README.html)
