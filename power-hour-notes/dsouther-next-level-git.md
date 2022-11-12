# Next Level Git

## Overview

Working in larger projects with git.

More people, more commits, longer histories, and more simultaneous commits and merges!

ACP: Shorthand for `Git Add` -> `Git Commit` -> `Git Push`

Git Branch:

- Manipulate branches.
- Create new, checkout existing, or remove branches in the repo.

Git Checkout:

- Change to an existing branch and start working in it.
- With `-b` create a new branch and then start working in it.

Git Commit:

- Store added file(s) to the current branch history.

Git Push:

- Takes local branch and copies to a remote using `git push targetRemoteName targetBranchName`
- `--force`
- `--force-with-lease`

Git Status:

- Tells you the state of the current branch.
- Also supplies hints on what commands or next steps make sense to do.

Pull Requests:

- A merge commit that is held until specific requirements are met, allowing users to comment, update code, or approve or request changes.
- Enables code-review by developers prior to merging commits into another branch, usually a main or staging branch.

Git Log:

- `--graph`: Displays what happened in ASCII graphical form with branches and commit log entries.

Git Rebase:

- Branch1: Trunk
- Branch2: From Branch
- Allows taking a branch and re-graphed it back into the trunk.
- This minimizes expanding branches outward, and keeps the trunk vertical, and easier to track.
- Git rebase abort: Backs you out of changes you feel should not be kept.

Git RefLog:

- Shows every commit you have ever stated.
- Helps get back to the place where the app worked prior to recent 
- `git checkout commitName`: Shows state

Git Reset:

- `git reset --hard commitName`: Forces the git history to be "rewound" to the identified commit.

## Key Takeaways

As projects get larger and larger, merge-commits get very complicated.

Conflict Markers:

- Two commits edit same lines of code.
- '<<<' markers indicate beginning of incoming conflicting commit.
- '===' markers indicate separation between the conflicting commit and current change.
- '>>>' markers indicate end of the existing conflicting current change.

## Footer

Return to [PPH Index](pph-index.html)

Return to [Root README](../README.html)
