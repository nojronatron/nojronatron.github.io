# Microsoft Copilot Learnings

These are notes taken while training on Microsoft Copilot technologies following this Microsoft Build event in May, 2024.

## Table of Contents

- [Build An Auto Suggest Engine Using Copilot](#build-an-auto-suggest-engine-using-copilot)
- [Intro to Copilot in MS Power Platform](#intro-to-copilot-in-ms-power-platform)
- [References](#references)
- [Footer](#footer)

## Build An Auto Suggest Engine Using Copilot

These notes were taken while working through MSLearn's Cloud Skills Challenge, Module "Guided Project - Build Auto Suggest Engine With Copilot".

### Auto-Suggest Project Objectives

- Interpret code with Copilot
- Author code with Copilot
- Debug code with Copilot

### Handy-Dandy Prompting

Use 'Explain This':

- Highlight code.
- Right-click and select Copilot and then select Explain This.
- Use Copilot Chat to tell it to explain the highlighted code line-by-line.

Use 'Generate docs':

- Highlight code.
- Right-click and select Copilot and then select Generate Docs.
- Use Copilot Chat to tell it to generate documentation for the highlighted code.

Prompt Copilot To Be More Specific:

- Add comments that specify what is wanted.
- `[Tab]` or `>` arrow through the Suggestions (assuming there is more than one).
- Highlight the method you want to know more about and then ask Copilot Chat to further describe the code.

_Note_: For some prompts, Copilot will offer to insert the code suggestion(s) for you, or allow you to copy it for pasting in yourself.

Copilot Helps You Write Unittests Rapidly:

- Write a comment begining with "Test that" (or similar) and wait for Copilot to do the rest.
- It might be necessary to add Attributes like `[Fact]` or `[TestMethod]`.
- Always review the code and use iterative Chat Prompts if the code needs revising to be correct.
- When writing Assertions, it might be necessary to use an in-line comment to describe it, then follow the next line with `Assert` and wait for suggestions.

_Note_: In VSCode, r-click the filename and select "Open in Terminal" and the Terminal will put you in that working directory. This is useful for running `dotnet test` from within a Test Project, rather than having to type the entire comand from the root of the Solution.

### Auto-Suggest Project Additional Takeaways

- Copilot's primary function is to assist in generating code and providing coding suggestions.
- Copilot might generate code that does not alight

## Intro to Copilot in MS Power Platform

## References

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
