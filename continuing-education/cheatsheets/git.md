# Git Cheatsheet

Keep a record of learned GIT tricks and traps.

## Checkout Workflow

[CSharp Fritz](https://twitch.tv/csharpfritz) used this flow on his Twitch stream one day:

1. Checkout a new branch: `git checkout -b {branch-name}`
1. Set upstream to remote: `git push -n origin {branch-name}`
1. Set a tag at the current commit: `git tag {new-tag-name}`
1. Push tag(s) to remote: `git push upstream main`

Key Takeaways:

- Name a Tag at any commit using the command line.
- Pushing a Tag to remote does not require opening a new branch or PR.

## Footer

Return to [ContEd Index](../conted-index.md)

Return to [Root README](../../README.md)
