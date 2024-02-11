# Publishing DotNET Apps

Various notes regarding application publishing in the .NET Ecosystem.

## Table of Contents

- [Versioning](#versioning)
- [Publish Self Contained](#publish-self-contained)
- [Publish Self Contained Command Line](#publish-self-contained-command-line)
- [ReadyToRun Images](#readytorun-images)
- [Ahead Of Time (AOT)](#ahead-of-time-aot)
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

The simplest deployment is `Framework-Dependent`:

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
- .NET 8 fewer limitations, still incomplete (see [References](#references))

Publish apps using Native AOT via the command line.

There are AOT-Compatibility Analyzers that can indivate whether a library is Native AOT ready.

## References

DevOps, Testing, and deployment documentation on MSLearn: [Publish Self-Contained](https://learn.microsoft.com/en-us/dotnet/core/deploying/?WT.mc_id=dotnet-35129-website#publish-self-contained).

Runtime Identifiers  on MSLearn: [.NET RID Catalog](https://learn.microsoft.com/en-us/dotnet/core/rid-catalog).

Overview of [.NET Native AOT](https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/?tabs=net8plus%2Cwindows).

## Footer

Return [Conted Index](./conted-index.html)

Return to [root README](../README.html)
