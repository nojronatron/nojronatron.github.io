# Github Copilot CLI Hands On

## CLI Basics

aka.ms/awesome-gh-cli-course

[GitHub Copilot CLI for Beginners course](https://awesome-copilot.github.com/learning-hub/cli-for-beginners/)

## Using AI Skills to Automate Repeatable Work

Renee Noble, Sr Dev Advocate, GitHub

Dave Glover, Principle Dev Advocate, GitHub

### Skills

On demand tools and instructions in the GH Cli toolbox:

- Task-specific functions and checklists
- Consisten results with recall
- Example: A template for generating tests
- Example: A function to convert image types

Written in markdown

- YAML Front matter has name and description properties
- Use headings to provide structure and order
  - Rules, Examples, Types, Format, specific language for Copilot to use, etc
- Can be:
  - Checklists
  - Knowledgebase
  - Template for tests or other resources
  - Scripts to run from the terminal
  - Processes and rules for making decisions
  - Any combination of the above
- Add Tools by adding "tools: []" to Skills.md

Write A Custom Skill:

- Directory Location
  - In `.github/skills/`
    - `skillname/`
    - `skill.md`

Add a skill:

- File: `/skill` tells you the CLI command to do this, source is a local file
- `/plugin install {URL or plugin-name@marketplace-name or owner/repo}`
- Alternate: `gh skill install github/awesome-copilot acquire-codebase-knowledge`
- NPX to install from GitHub: `npx skills add github/repo-name@skill-name -g -y`

After adding a Skill:

- Tell copilot CLI to reload skills: `/skills reload`

### Agents

- Take on a persona to orchestrate workflow logic
- Applies reasoning patterns and specific domain knowledge
- Selects skills/tools to use to progress to a goal
- Example: Act as an expert frontend developer

### MCP Servers

Connect to an external server in real time:

- Connect to live data from external sources
- Provde on demand context
- Example: GitHub Issues
- Example: Databases
- Example: Docs

## Resources

- There is an existing Skill called "Microsoft Skill Creator" that can be downloaded/installed to help teach GH Cli about any MS technology.
- [Copilot Agent Skill Customization Instructions](code.visualstudio.com/docs/copilot/customization/agent-skills)

## Footer

Return to [Conted Index](../conted-index.md)
