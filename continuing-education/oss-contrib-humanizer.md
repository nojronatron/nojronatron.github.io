# OSS Contribution - Humanizer

I started looking into open-source contribution opportunities after watching an overview of GitHub Repositories (of all things), and during the presentation, I provided some answers to a few of the attendees questions regarding OSS.

To start, this will be just an investigation.

In the future, the investigation could turn into a contribution attempt, and will be documented accordingly.

## Oveview

Humanizer is a Library with the goal of "manipulating and distplaying strings, enums, dates, times, timespans, numbers and quantities" [About Humaziner](https://github.com/Humanizr).

I can see this NuGet Package being useful in my current and future projects, especially in cases where a more sensible Date or Time display is needed, or converting various types of inputs from a form or REST should be converted in various ways.

## Project Analysis

The Humanizr / Humanizer repo is fairly active, currently:

- 23 Releases, latest on 23-Mar-2024.
- 447 closed Issues and 136 open: Newest 15-Mar-2024, oldest 9-Apr-2024. :astonished:
- Over 800 closed PRs and 15 open, ranging in age from late March 2024 to late Sept 2017. :thinking:

The README is pretty easy to understand, guiding the reader through installation, supported frameworks, and a lot of usages for specific languages (en is default) or collections of languages. There is a section that shows a concrete example of using the Humanizer Package Features, and provides links to resources of related projects for Java, PowerShell, Node.js, and ReSharper Annotations.

Build automation is provided in Azure DevOps Pipelines.

The project has an MIT License file, allowing usage, modifiction, and distribution, provided inclusion of the License File.

> Before going any farther investigating any Humanizer Issue(s), the following GitHub Issue should probably be resolved [Is This Library Still Maintained?](https://github.com/Humanizr/Humanizer/issues/1303).

### Contributing

Contributing guidelines are in the `.github` directory, in CONTRIBUTING.md.

In summary:

- Raise bugs as Issues in GitHub (or fix and Pull Request).
- Grab and fix any Issue.
- `Jump In` labeled Issues are considered "low hanging fruit".
- Code of Conduct exists and follows `Contributor Covenant`.

#### Contributing Getting Started

- C# 8 language features.
- SDK-style projects.
- VS 2018 or newer.

#### Guidelines

Overview:

- There is a checklist of code style requirements to meet (see `.editorconfig` and [PULL_REQUEST_TEMPLATE.md](https://github.com/Humanizr/Humanizer/blob/main/.github/PULL_REQUEST_TEMPLATE.md)).
- PRs with ReSharper Warnings will not get merged in.
- Unit Tests required, w/ coverage.
- Full disclosure and attribution required for any copied code.
- Few (if any) code comments.
- XML Documentation must be updated with change(s).
- Sync with upstream before rebasing.
- Rebase PR on top of main before submitting.
- Link to Issue(s) the PR addresses.
- Update README as applies.
- Build not *not* have any failures.

## Solution Overview

- The software is a set of Projects attached to a parent Solution file.
- There appear to be some custom build and test scripts.
- Test Project exists that appears to use XUnit, relying heavily on `[Theory]` annotated tests with canned inputs and expected outputs in `[InlineData()]` annotations.
- Humanizer.csproj is the primary, central-focus project.
- Humanizer.InflectorExtensions.cs has a number of static Extension methods that perform actions like pluralize, singularize, Titleize, Pascalize, and more.

## Issue Description

The Issue in focus for this write-up is [Problem in Camelize method](https://github.com/Humanizr/Humanizer/issues/1397).

The assertion is that the Camelize function should accept string input, and return a `camelCase` result for every input.

Examples (`sampling from Humanizer.Tests.InflectorTests.cs`):

- "customer": "customer"
- "CUSTOMER": "cUSTOMER"
- "customer_first_name goes here": "customerFirstNameGoesHere"
- "customer name": "customerName"
- (There are more)

The Issue asserts that an input like the following is not processed correctly:

- Expected: "some-text-here" :arrow_right: "someTextHere"
- Actual: "some-text-here" :arrow_right: "some-text-here"

In additional comments, it is noted only alphanumeric characters should be returned, excluding any hyphen or underline between words.

## Initial Code Analysis

Looking at `Humanizer.InflectionExtensions.cs`, the function in question is defined as `public static string Camelize(this string input);`.

- Leverages `Humanizer.InflectionExtensions.Pascalize` static extension method to do most of the work.
- `Pascalize` peforms a Regex Replace, matching the first letter in each capture Group and returns that character as an Upper-case character.
- `Camelize` then looks at the first character in the string returned by `Pascalize`, performs a `Substring()` to find the first charcter of the string, applies `ToLower()` to that one character, then concatenates the SubString and the original String (minus the first character) as the result.

### Dependencies

Humanizer is targeted as a NuGet Package, and its Project targets several DotNET versions:

- dotnet48?
- dotnet6.0
- dotnet7.0
- dotnet8.0
- NetStandard2.0
- BenchmarkDotNet

These dependencies have their own dependencies (not in any order):

- Nerdbank.GitVersioning
- Polyfill
- System.Collection.Immutable
- System.Memory
- System.ValueTuple
- NETStandard.Library
- System.ComponentModel.Annotations

Even the XUnit Tests have multiple dependeny Packages:

- coverlet.collector
- Microsoft.NET.Test.Sdk
- Nerdbank.GitVersioning
- PublicApiGenerator
- Verify.DiffPlex
- Verify.Xunit
- xunit
- xunit.runner.visualstudio

### Initial Thoughts

Some naive thoughts about the code under analysis, after only reviewing the specific method, and without building, running, or 'using' the Package at all:

- Since Camelize relies on Pascalize, it is possible other members also rely on either or both of these methods, which could result in more risky code change to fix.
- `RegEx.Replace()` method is used without any constraints, and the input could potentially be an end-user provided string. This could lead to a risk of an endless loop that could cause an Application crash.
- The static extension methods provide summary descriptions in code comments, but no obvious indication that they might throw an Exception.
- The static extension methods do not have any Try-Catch structures in them.
- Why are the repo owners committing directly to main?

*Note*: The above comments are simply front-of-mind and are no way intended to be negative commentary about code style, structure, stability, capability, or security of Humanizer or its contributing developers. These thoughts are out there as a means to help guide my analysis and (any) future actions I might take to try and resolve the problem.

### Problem Domain Diagram

Future: A diagram of the argument flow and code processing.

### Scope

Future: A brief on how to avoid introducing more bugs while developing a well-scoped solution to the problem under analysis.

## Actions

Future: A brief on what actions I take (and why), when it happens. Any additional status information will be added if/when action is taken.

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
