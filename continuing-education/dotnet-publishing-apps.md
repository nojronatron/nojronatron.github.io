# Publishing DotNET Apps

Various notes regarding application publishing in the .NET Ecosystem.

## Table of Contents

- [Versioning](#versioning)
- [Publish Self Contained](#publish-self-contained)
- [Framework Dependent](#framework-dependent)
- [Publish Self Contained Command Line](#publish-self-contained-command-line)
- [ReadyToRun Images](#readytorun-images)
- [Ahead Of Time (AOT)](#ahead-of-time-aot)
- [Building Visual Studio Extensions](#building-visual-studio-extensions)
- [References](#references)
- [Footer](#footer)

## Versioning

This note was started on 16-Jan-2024:

- Use referenced resources for the latest information.
- Initial target is .NET 6 (subsections may cover .NET 8 or others).

## Publish Self Contained

Publish Self-Contained means:

- Produce a platform-specific executable.
- All .NET libraries and target runtime are included.
- App isolation from locally-installed runtimes.
- User does _not_ have to download and install different .NET version or runtime!

Drawbacks:

- Larger portable installer file size.
- Upgrading .NET version requires new self-contained publish.

## Framework Dependent

The simplest deployment type:

- Cross-platform.
- Smaller package size (do not include .NET runtime), so user must install if not already has.

Note: NuGet Package dependencies could still be platform-specific.

```powershell
# cross-platform and framework-dependent
dotnet publish

# platform-specific and framework-dependent
dotnet publish -r win-x64

# platform-specific and framework-dependent for linux
dotnet publish -r linux-x64
```

## Publish Self Contained Command Line

Use the `dotnet` `publish` command with argument `--self-contained`:

```powershell
dotnet publish --self-contained
```

Specify the target:

- Platform Moniker (not marketing name).
- Version: Dot-separated like `15.10`.
- Architecture: Use the `-r <RID>` parameter.

```powershell
# Windows 64-bit
dotnet publish -r winx64 --self-contained

# Windows 32-bit
dotnet publish -r win-x86 --self-contained

# Windows arm64
dotnet publish -r win-arm64 --self-contained
```

RIDs need to be _specific_:

- Do NOT try to parse RIDs to retreive component parts.
- Only use RIDs that are _already defined for the target platform_.

## ReadyToRun Images

These will improve startup time but will produce an even larger installer file, and do _not_ contain the JIT.

```powershell
dotnet publish -c Release -r win-x64 --self-contained -p:PublishReadyToRun=true
```

## Ahead Of Time (AOT)

Just a quick list of notes:

- Requires _.NET 7_+
- Console apps _only_ in .NET 7
- Limited libraries available in .NET 7
- .NET 8 fewer limitations, still incomplete (see .NET Native AOT in [References](#references))

Publish apps using Native AOT via the command line.

There are AOT-Compatibility Analyzers that can indicate whether a library is Native AOT ready.

## Building Visual Studio Extensions

VS Code has a special tool called _VSCE_ for Packaging Pre-Release and Release packages in the VSIX format for use in the Visual Studio Marketplace.

- Developing in JavaScript is very similar to any other JS or Node-based development workflow: Use `NPM` or `Yarn` to add dependecies or dev dependencies, and update `package.json` to configure scripts and basic features of the project.
- VSCE can be installed using npm: `npm i @vscode/vsce`.
- VSCE can utilize package.json to get product details such as `display name`, `description`, `icon`, `repository`, `version`, `publisher`, `pricing`, `categories`, and much more.
- VSCE leverages `.vscodeignore` to filter-out files that are not necessary in the package itself. It is good practice to reduce the file size as much as possible by eliminating all but the absolutely necessary files.

- Pre-release and push to the Visual Studio Marketplace: `vsce publish -p { vsce_pat } --pre-release`

It is important to note that README.md is used as the _Details_ page view within the Extensions view in VS Code. Excluding files using `.vscodeignore` does _not_ remove the files from the appearance in the Marketplace or Extensions viewer.

### Publishing With VSCE

In order to push a Package to the VS Marketplace, the following must be true:

- `package.json` `version` element must be above any existing Published version in the VS Marketplace.
- `publisher` element in `package.json` must match an existing VS Marketplace Publisher.
- The `Private Access Tocken` (PAT) must be associated with the configured VS Marketplace Publisher.

Note that VSCE has some interesting default behavior:

- Running `vsce package` will use the existing `package.json` `version` element during its packaging process.
- Running `vsce publish` is very similar to `vsce package` except it automatically tries to increment the `package.json` `version` element and execute `npm i`, then tries to push the package to the VS Marketplace automatically. If a PAT has not been included, the command could prompt for one.

### Publishing To Visual Studio Marketplace

Automatic publication of Release or Pre-Release versions is possible using VSCE.

It is also possible to manually package the Extension with VSCE, login to the VS Marketplace mangaement portal, and then upload the VSIX file in just a few clicks.

Either way, VS Marketplace will take a few minutes to process the file.

The next time a user opens VSCode, they will see a notification for each new Release (and might see notifications for Pre-Releases, if they've opted in).

### VSCode Ignore Suggestion

```markdown
.vscode/**
.vscode-test/**
test/**
.gitignore
.yarnrc
vsc-extension-quickstart.md
**/jsconfig.json
**/*.map
**/.eslintrc.json
**/*.ts
**/tsconfig.json
```

## Build Test Publish Workflow for Create TOC

While building the Create Table of Contents VS Code Extension, a workflow developed based on:

- Reading [Testing Extensions](https://code.visualstudio.com/api/working-with-extensions/testing-extension).
- Reading [Publishing Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension).
- Exercising [GitHub Actions YAML](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions).
- Leveraging Terminal commands to perfom actions locally such as with NPM and VSCE tools.

Tools:

- Mocha: Unittest framework supporting all add-on module testing.
- NPM: Execute build, lint, test, and package operations locally.
- GitHub Actions: See `.github/workflows` for the automated unittesting and packaging YAML scripts.
- VSCE: Manual packaging and publishing tool.

Branching:

- Create a development branch for the task at hand (new feature, bug squashing, etc).
- Staging branch: Merge new development here for preparation to publish.
- Pub-Pre-Release branch: New PR's to this branch after updating version info to push a Pre-release Publish to the VS Extension Marketplace.
- Main branch: This is the default branch and is what is viewable on the GitHub Repo page.

Workflow:

1. Develop new features, updates, or bug-fixes to a custom branch.
2. Update unittests to cover module functionality and regressions.
3. If a Module has multiple interrelated functions, ensure an integration test is developed to verify expected behavior.
4. Create a PR to merge with `Staging` branch.
5. Once the feature (milestone, bug fix, etc) are well tested the PR can be merged-in to `Staging`. Workflows run unittests and pass/fail PR approval.
6. Documentation and versions are updated in `Staging` branch and a new PR is created to merge with `pub-pre-release` branch.
7. A workflow runs that executes unittests and pushes a Pre-release version to the VS Extension Marketplace Publisher's portal.
8. Once the Pre-release version has been tested in the field, update the version info to a private branch (for now) that has the latest `pub-pre-release` branch commits, and manually execute VSCE to produce a Release Publish package that can be manually uploaded to the VS Extension Marketplace Publisher Portal.
9. The private (for now) publish branch gets merged-in to `main`.
10. Optional: The GitHub `Releases` page could be updated to allow downloading the latest Release VSIX file for manual importation and use.

_Note_: Step 8 should eventually get updated to a proper branch workflow with an automated Release operation.

_Note2_: Step 10 could be automated to push the `VSIX` artifact to the GitHub `Releases` page.

### Package and Publish VSIX by Hand

1. Ensure the following are up to date: `package.json`, `CHANGELOG.md`, `.gitignore`, `.vscodeignore`, and `README.md`.
2. In the Terminal, execute `npm i`. All installations should complete with out Security Issues or other errors.
3. In the Terminal execute `npm test`. All Linting and Tests should pass before continuing.
4. In the Terminal execute `vsce package --no-update-package-json {major.minor.patch}` and the output file will be named `{package_json_name}-{major.minor.patch}.vsix`.

_Note_: To auto-increment the version number, just run `vsce package` and `package.json` will get updated with an incremented `version` property.

_Note2_: VSCE includes options `login <publisher>` and `publish [options] [version]` to allow publishing _directly_ to the VS Extension Marketplace.

_Note3_: `publish` and `package` commands are _very similar_ so it is possible to publish a version without adding a version control change.

## References

DevOps, Testing, and deployment documentation on MSLearn: [Publish Self-Contained](https://learn.microsoft.com/en-us/dotnet/core/deploying/?WT.mc_id=dotnet-35129-website#publish-self-contained).

Runtime Identifiers in the MS Learn [.NET RID Catalog](https://learn.microsoft.com/en-us/dotnet/core/rid-catalog).

Overview of [.NET Native AOT](https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/?tabs=net8plus%2Cwindows).

## Footer

Return [Conted Index](./conted-index.html)

Return to [root README](../README.html)
