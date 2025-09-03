# Playwright Notes

## About

Modern testing framework.

Supports:

- Any browser, any platform.
- Nodejs, Python, DotNET.
- Chromium, Firefox, and WebKit support.
- Android apps too!

Manual and Automated:

- Direct the test scenario.
- Use scripts to drive UI testing.

Runs in isolation:

- No test-to-test leakage.
- Browser restart takes time, so Playwright uses Browser Context with pages to quickly tests w/o browser restarts.

Playwright Tracing:

- List all steps performed.
- Timeline of steps included.
- Also snapshots the site with full DOM access.
- Console, Network, and Source views available.

Getting Started:

- `dotnet add package microsoft.playwrite.mstest`
- Libraries and browsers still need to be installed.
- Chromium, FF, and WebKit get installed using the installation script in a Terminal.
- Build unittests in an MSTest file.
- Playwright launches browser in 'headless' mode, this can be changed.
- 'Headed Browser' execution speed can be slowed using 'slowMo=nnnn' command when launching.

GitHub Integration:

- Supports GH Actions!
- Define the Playwright Execution in YAML.
- Set rules to determine when, and which Playright tests to execute.

## PGH.NET Presentation: The Power of Playwright

Host:

- PGH.NET: Pittsburgh DotNET User Group
- The DotNET Foundation

Presenter:

- Randy Pagels, Prin Trainer, Xebia USA
- Xebia | Microsoft Services

### Challenges

- Learning frameworks
- Testing is hard to get right
- Building tests takes time

### Modern Testing Goals

- Easy
- Fun
- Fast feedback loop
- Painless test development
- Complement dev workflows
- Integrate with CI/CD pipelines
- Simplify testing at scale

### Automation Best Practices

- All tests are independent, without chaining
- Clean setup and clean-up phases
- Framework should point to reason why tests fail, for example: screenshots
- Self-describing tests
- Not _all_ tests need to be automated, use the 80-20 rule here

### Playwright Architecture

- Language bindings
- Single automation protocol
- Unified debugging protocols
- Native browser debugging protocols, tools

### Use Playwright With

- Modern browsers
- VS Code, Visual Studio (others?)
- Github Actions Pipelines
- Visual Studio Test Runner extensions

Note: Does _not_ support desktop apps such as WPF.

### Features

- Code-generation in 'Record' Mode: Manually drive the test, ending with a replayable test. Manually add the ending assert(s).
- Cherry-pick specific test files to execute
- Test listing and test execution reporting at the Terminal
- Trace On: Gathers videos, screenshots, and test results for bulk execution and review
- GUI App also lists tests, allows execution, reporting on pass/fail, errors, etc
- Playwright MCP Server: Copilot can build Playright Tests for you
- JS/TS, Python, C#, Java
- Chromium, Firefox, Webkit

### Azure App Testing Service

- Load Testing + Playwright Testing
- Test at scale
- Reports following execution

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
