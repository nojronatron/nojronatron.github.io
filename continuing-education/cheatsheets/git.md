# Git Cheatsheet

Keep a record of learned GIT tricks and traps.

## Table of Contents

- [Checkout Workflow](#checkout-workflow)
- [Set Upstream](#set-upstream)
- [Tagging](#tagging)
- [Git Reset](#git-reset)
- [Footer](#footer)

## Checkout Workflow

[CSharp Fritz](https://twitch.tv/csharpfritz) used this flow on his Twitch stream one day:

1. Checkout a new branch: `git checkout -b {branch-name}`
1. Set upstream to remote: `git push -u origin {branch-name}`
1. Stage changed files: `git add {...filename | .}`
1. Commit staged changes and add a comment: `git commit -m '{50-char-un-truncated-comment}`
1. Push changes to remote:  `git push`

Key Takeaways:

- Use remote tracking by using the `-u` flag to simplify future push commits by using just `git push`
- If remote tracking is not enabled, use `git push {remote-name} {branch-name}` but make sure you get the branch-name correct.

## Set Upstream

Two common ways:

1. When setting up a new branch.
2. When adding a remote branch to your local.

### Set Upstream To New Branch

1. `git checkout -b {branch-name}`
1. `git push -u origin {branch-name}`
1. Start deving and git flowing.

### Add Remote Branch To Local

1. `git checkout -b {remote-branch-name}`
2. `git branch --set-upstream-to={remote}/{remote-branch-name} {remote-branch-name}`

For example:

- A common trunk branch named "staging" exists remotely.
- Your remote repository is named "origin".
- You need a local copy of staging branch to weed out merge conflicts before creating a PR.

1. `git checkout -b staging`
1. `git branch --set-upstream-to=origin/staging staging`

## Tagging

1. Set a tag at the current commit: `git tag {new-tag-name}`
1. Push tag(s) to remote: `git push upstream main`

Key Takeaways:

- Name a Tag at any commit using the command line.
- Pushing a Tag to remote does not require opening a new branch or PR.

## Git Reset

Terminal usage example: `git reset --{option} {commit_hash}`

Options:

- Soft: Removes the last commit from current branch, retaining file changes `git reset --soft HEAD~1`
- Mixed: Same as soft _except_ retains changes in working tree but _not in the index_ (unstaged) `git reset --mixed HEAD~1`
- Hard: Lose all uncommitted changes, including untracked files. This effectively rolls-back the commit _and all file changes_ to the previous commit `git reset --hard HEAD~1`
- Merge: Undo a _merge_ while preserving uncommitted changes in current working directory.
- Keep: Similar to Hard but uses a _diff_ against all files so uncommitted changes are _not reset_.

Visual Studio:

- Mixed: Pick the commit **just prior** to the one you want to reset and it will store changes to tracked **unstaged** files

## Footer

Return to [ContEd Index](../conted-index.md)

Return to [Root README](../../README.md)
