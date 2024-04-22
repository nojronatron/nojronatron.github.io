# DotNET Community Standup - Simplifying .NET Development

## Overview

Hosts:

Bill Wagner, C# Content
Kathleen Dollard, .NET Languages PM, MSFT
Chet Husk, .NET SDK PM, MSFT

Guest Speaker: Mikayla Hutchinson, on the .NET PM Team, MSFT

## Discussion Notes

For those who are new, how to get started?

DotNET can seem very large and overwhelming.

Fast-paced (yearly) features updates and conceptual changes have made .NET complex.

Onboarding for new users can feel like a very steep climb (or a terrible cliff fall).

New Visual Studio XML-based solution file format just released:

- Newly updated, simplified solution file format in XML instead of UTF-8.
- File extension 'slnx'.
- Actually a preview release.
- [Welcome to the new Visual Studio SLNX Solution File](https://schwabencode.com/blog/2024/04/10/welcome-new-visual-studio-slnx-solution-file) by Ben Abt [BenjaminAbt on GitHub](https://github.com/BenjaminAbt).

If globbing for solution files when building and running, is the solution or project file even needed anyway?

Terminology challenges:

- SDK: Is this installable .NET SDK or MSBuild SDK?
- Other ambiguous or easily, overloaded terms exist.

Project Templates:

- Good: Help ensure new projects have good defaults.
- Not so good: Many projects do not utilize the defaults, adding a feeling of more complexity.
- Best, recommended settings in Project files means the Project file is _more complex_ than those that don't.
- DotNET warns that enabling 'nullable' support is guaranteed to break too many existing projects and therefore too disruptive, so it shouldn't be enabled by default.

Adjusting Project File syntax or enabling other syntax and configuration files (format):

- Challenges exist with integrating into the rest of the tooling if Project configuration is in alternate format.
- There is a proposal for YAML or JSON formats, but it is not in the pipeline yet.
- The Project Files are pretty much declarative, however there are programmatic sections as well. Should those be split when using a different syntax?

DotNET Framework Support Lifecycle?

- VERY Long support is planned for this.
- Will _not_ get newer features, patches, etc.
- More tools will be delivered to help transition to transition to newer .NET versions.
- Much of the work .NET that is done is maintaining compatibility and support.

## Closing

There is a lot more going on than what was discussed here. Much of it over my head (but not too far). Essentially, there is potential for a new transformation of how project files are built and used, more information and support on .NET upgrade/migrations, and managing build props and parameters, behaviors (functional definitions), and project tooling.

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
