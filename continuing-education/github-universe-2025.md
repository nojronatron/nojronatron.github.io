# Github Universe 2024

Random notes taken while virtually attending GHU'24.

"The world's fair of software"

## Table of Contents

- [Keynote Wednesday 29-Oct-2025](#keynote-wednesday-29-oct-2025)
- [Keynote Tuesday 28-Oct-2025](#keynote-tuesday-28-oct-2025)
- [References](#references)
- [Footer](#footer)

## Keynote Wednesday 29-Oct-2025

Presenter: Martin Woodward, VP Dev Relations, GitHub

People give software a soul:

> "Dream in the morning, build it in the afternoon."
> "Every tool shrinks the distance from idea to MVP."
> "Collaboration drives progress - people talking to other people."

- Projects are (often) willed into existance because someone had (an idea).
- With Copilot, you write the story, it writes the code.
- Code the tool(s) you need.
- What if moments inspire teams to make change, impacting many users.
- Missing framework, library, or module? Ask Copilot to build it for you.

> "The distance between a silly idea and a world changing one is perspective."

### HackClub Team Presentations

Hackathons are:

- Supported by GitHub.
- Hives of "dreaming in the morning and building in the afternoon".
- Hubs of learning new skills and technologies.

#### (project)

- Jaden Monney, Crazy Controllers
- Elliott Preston

Glove with sensors assist translating sign language in real time.

#### CrisisLens

Brian Park
Alethea Kramer

- P2P
- Live-streaming
- Emergency and other incidents mapping and information collector.
- Automatic connecting to live streams, acquired through map clicks.

#### Braillearn

Cindy Cui
Alison Co

- Braille displays, devices are expensive.
- Physical box raises braille representations of characters.
- Learning tool.
- Speech recognition encodes braille.

### Tiny but Mighty Wins

Guest: Helen Hou- Sandi, GiHub

- Fixed merge conflict UX on GitHub.com! _thank you_!
- "Scratch your own itch."
- Fix all the little annoying things that bug you, reducing the million paper cuts problem.
- Collaboration is necessary.
- Outside complexity often slows fixing papercuts.

### Using GitHub Tooling and Managing Change

Guest: Dylan Morley, Distinguished Engineer, ASOS

- Manual tasks were automated using Copilot Agent Mode.

### Open Healthcare Network

Guest Presenters:

- Bodish Thomas, Head of Digital Public Goods, Open Healthcare Network
- Gigin Chandy George, Engineering Lead, Open Healthcare Network

Notes:

- Curiosity started the idea to build OHN.
- Draw the UI and let Copilot do the work asynchronously.

## Keynote Tuesday 28-Oct-2025

Presenter: Kyle Daigle, COO, GitHub

"Change is the only constant."

### Stream of Notes

Coding Agents:

- Only 18 months old!
- Many new and existing features available with paid Copilot subscription.
- Async, multi-task workflow capabilities.
- New: Agent HQ. Integrates Agents into workflow to review, revise, continue work, in parallel, asynchronously.
  - Supports all coding agents (Claude, OpenAI, etc).
  - Will support newer 3rd party Agents going forward.
- Secrets Validators: Check and validate Secret detection, validation, and notification.
- MCP Servers and GH MCP Registry simplify app and service integration.
- New Today: Copilot Coding Agent runs on self-hosted Actions runner.
- AgentHQ: The AI Agent Control Plan.
- "VSCode is the #1 project for 1st-time OSS contributors on GH." *[Kyle Daigle]*

Slack: Integrated Copilot Agent tasking.

Code Review:

- Core part of developer's job.
- CP reviews code already.
- New: Agentic Copilot Code Review using CodeQL, Linters, etc.
- Custom Instructions :plus: CP Code Review :arrow-right: agentic AI bug finding and review completion (in record time).
- Captures security issues and suggests fixes: Mention `@copilot` and it will spin-up a new PR where security vulnerability is addressed.

Copilot Metrics Dashboard:

- API Access and metrics dashboard to view progress.
- Public Preview now available on paid Copilot subscriptions.
- Copilot :plus: _any coding agent_.

Govern Agent Workflows:

- Single Admin interface for Agent access controls.
- New Role defined to enable mobile, web, and Coding Agent managing access control of features.

### Guest Presenter: Jessica Deen, staff dev advocate, GitHub

- Paid Copilot subsription features available today:
- GitHub Agents Panel: Accessible on your GitHub Repo, next to Search.
- Custom Agents Integration: Allows GH Customers to add their Agent(s) with Copilot Coding Agent.
- Supply feedback to Copilot _while it is processing_ to "steer" its session.
- Built-in Code QL, Linters, and Secrets protection during processing sessions.
- Integrated Playwright MCP enables Agent to test its own code and display screenshots of its session progress.
- Start building on the web, continue on local editor.

### Guest Presenter: Mike Krieger, Chief Product Officer, Anthropic

- Claude is native collaborator in AgentHQ.
  - Claude Agent SDK.
- Claude Skills: Scripts and tools that help Claude complete tasks.
  - Example: Define Brand Guidelines once, Claude applies to all future code changes so they meet corporate standards.
- Goal: Available by end of 2025.

### Guest Prsenter: Alexander Embricios, Product Lead for Codex, OpenAI

- VSCode Extension Codex: 'Engineering Teammate'
- Auto Compaction: Model and Context Window are managed so that much larger problems can be solved.
- Parallelism: Multiple Codex Agents can solve multiple coding problems on the same codebase simultaneously.
- Available in Preview in VSCode for insiders.
- Will be available in AgentHQ in 2026.

### Guest Presenter: Pierce Boggan, PM Lead, VS Code, MSFT

- Plan Mode: Agent plans, with your refinements - a "Collaborative Design Partner" *[Pierce Boggan]*
- Select "Plan" from the Agent Modes selector.
- Can pass plans to Coding Agent to implement the code in a session.
- Developer can implement Agent Instructions with "tools" definitions so Copilot can be more effective at fixing red squigglies, etc.
- Copilot can asynchronously experiment on coding, feature ideas.
  - Provide ideas on different approaches or ideas for a feature.

### Guest Fireside Chat

Guests:

- Satya Nadella CEO, MSFT
- Jared Palmer, SVP, GitHub
- (another presenter, TBN)

Stream of Thought:

- "Moments in shift in developer toolchain."
- "Next level of abstraction."
- "Cognition and meta-cognition around code."
- Vide Coding creating 'slop' "...is a problem".
- More tools seems to result in more artifacts:
  - How to reduce the chaos and improve the success around using the tools to build the solutions.
  - Wiring everything together is a challenge, but is the job of MSFT and GitHub to address this challenge.
- Exponential growth of LLM:
  - So fast but difficult to manage small (and large) errors.
- MSFT was born as a Developer Tools Company:
  - A software factory that builds tooling for other software factories (sic, Satya).
- MSFT is a Platform Company:
  - Platform is often an overloaded term.
  - Intrinsics and the design of intrinsics that others can build upon.
  - And recognize how platforms and partnerships rapidly build value.
- As code as input, what are we going to create as output?
  - The _how_ has changed, while the _what_ is relatively the same.
  - Focus effort on how the toolchain is used to drive artifact outputs.
  - Good to understand _how_ to do it not just the _what to do_.

## References

## Footer

Return to [ContEd Index](./conted-index.md)

Return to [Root README](../README.md)
