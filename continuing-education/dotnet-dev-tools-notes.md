# DotNET Developer Tools

Notes taken on many topics related to common .NET Dev Tools including:

- Dev Home
- Dev Drive
- Windows Package Manager
- PowerToys
- WSL and WSL-2

...and possibly more.

## WinGet

Is a command-line application and package management tool.

- Similar purpose to Linux `apt` or `pkgmgr`

Install WinGet:

1. Windows 10 and 11
2. Add/update AppInstaller via Microsoft Store

Developer option: Install a preview version of WinGet

Windows Sandbox:

- Lightweight environment isolates software.
- Windows Sandbox must have WinGet installed using posh script (see "Using WinGet" link for that script).

WinGet Preview can be downloaded for Windows Sandbox instead of the release version.

Note: Admin priviledges might be required to install and/or execute, depending on environment, and whether Admin was used to install WinGet in the first place.

### Basic Usage

- `winget` in a terminal/posh
- Basic WinGet info: `winget -v` and `winget --info`
- Search availabile tools: `winget search {appName}`
- Install: `winget install {appName} {appName}...`
- Show App details: `winget show {appName}`
- Change sources: `winget source {command}`
- Validate package manifests: `winget validate {args}` 
- Get help: `winget --help`

### Supported Installers

EXE, ZIP, INNO, NULLSOFT, MSI, WIX, APPX, MSIX, BURN, PORTABLE.

### Other Notes

- As of this writing, there are many partially-implemented or buggy features due to the early-release nature of the tool.
- Tools can be added via the Community Repository.
- Debugging and troubleshooting tools are available for WinGet packages.
- Use `settings.json` to customize WinGet settings.
- WinGet _is open source_.

After some quick investigation online, it looks like WinGet can be used to integrate into CI-Cd pipelines. More research will be necessary to discover the what, how, and when details.

### WinGet Configuration Overview

Importing configuration files:

- Machine setup and project onboarding: Unattended, repeatable setup and configuration.
- Leverages YAML, posh DSC automation, and Windows Package Manager to setup machine and onboard projects.
- Utilize DevHome to import an existing WinGet config file or use `winget configure` (v.1.6.2631+) to import and apply a configuration.

Declarative, not imparative:

- YAML file defines configuration state
- Desired state is declared as the target final result/state

Importation behavior:

- Configure files are parsed for validity
- Necessary posh modules are downloaded to support DSC automation
- Tests are run on each declaration in config, then DSC applies the declared state items
- Install and configuration operations will occur in parallel (ordering YAML entries is not necessary)

## References

- [WinGet GitHub Repo](https://github.com/microsoft/winget-cli/).
- Using [WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/).
- See my MSFT Build 2024 notes on [Windows Subsystem for Linux](./msbuild-2024-notes.md#windows-subsystem-for-linux-your-enterprise-ready-multitool).
- See my MSFT Build 2024 notes on [DevBox](./msbuild-2024-notes.md#level-up-with-devbox).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
