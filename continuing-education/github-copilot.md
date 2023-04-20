# GitHub Copilot

Liam Champton @liamchampton

Kory - Cloud Advocate @koreyspace

## Overview

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

## References

[General Links](https://aka.ms/levelup-links) from 'Level Up Your App Development Using GitHub Copilot and Codespaces' MSFT Reactor Session.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
