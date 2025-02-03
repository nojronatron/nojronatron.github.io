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

## Git Reset

Usage example `git reset --{option} {commit_hash}`:

Options:

- Soft: Removes the last commit from current branch, retaining file changes `git reset --soft HEAD~1`
- Mixed: Same as soft _except_ retains changes in working tree but _not in the index_ (unstaged) `git reset --mixed HEAD~1`
- Hard: Loose all uncommitted changes, including untracked files. This effectively rolls-back the commit _and all file changes_ to the previous commit `git reset --hard HEAD~1`
- Merge: Undo a _merge_ wile preserving uncommitted changes in current working directory.
- Keep: Similar to Hard but uses a _diff_ against all files so uncommitted changes are _not reset_.

## Footer

Return to [ContEd Index](../conted-index.md)

Return to [Root README](../../README.md)
