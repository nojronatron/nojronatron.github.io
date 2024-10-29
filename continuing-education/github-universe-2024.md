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

## Resources

## Footer

- Return to [ContEd Index](./conted-index.html)
- Return to [Root README](../README.html)
