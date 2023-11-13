# GitHub Copilot

Liam Champton @liamchampton

Kory - Cloud Advocate @koreyspace

## Table of Contents

- [Overview](#overview)
- [Codespaces](#codespaces)
- [Copilot](#copilot)
- [The GitHub Next Team and Project](#the-github-next-team-and-project)
- [References](#references)
- [Footer](#footer)

## Overview

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

## References

[General Links](https://aka.ms/levelup-links) from 'Level Up Your App Development Using GitHub Copilot and Codespaces' MSFT Reactor Session.

Check out [GitHub Next](https://githubnext.com) for information on what the GitHub Next team is working on.

Developing [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
