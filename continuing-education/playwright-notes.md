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

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
