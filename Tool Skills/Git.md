# git

## Git Bash

### Setting up

`git init` - Initialize repo.

`git remote add <name> <remote-repo-url>` - Connects local repo to the remote one. Name is usually a short alias like `origin`, `upstream`, `production`.

`git clone <repo-url>` - Copy a remote Git repo and automatically set the local main branch to track the remote main branch.

### Saving changes

`git add <file>` - Stage changes for commiting.

`git restore [--staged] <file>`- Reverts files to a previous state before editing.
- `--staged`: Unstage files staged for commit.

`git stash` - Temporarily save uncommitted staged and unstagged work.

`git commit -m "message"` - Save snapshot.

### Reviewing

`git status` - Check state.

`git log [--oneline] [--graph] [--all]` - View history.

`git branch [-vv] [-r]` - List branches.  
- `-vv`: Displays the remote branch that the local branch is tracking.  
- `-r`: List remote branches.

`git remote [-v]` - List names for configured remote repos.
-`-v`: Show the URLs for fetching and pushing for each remote.


### Branching

`git branch [-d] <branch-name>` - Create new branch.
- `-d`: Delete branch.

`git switch [-c] [--track] <branch-name>` - Switch to branch.
- `-c`: Create new branch and switch to it.
- `--track`: Create new local branch tracking a remote branch (upstream) with the same name.

`git merge <branch-name>` - Merge branches in a new commit.

`git rebase <branch-name>` - Add commits from the branch to the current branch without creating merge commit.

### Remote

`git push <remote> <branch>` - Push local branch to the specified remote. Without any arguments it pushes the current branch to its upstream.

`git fetch [--prune] <remote>` - Fetch updates.
- `--prune`: Prunes deleted branches from the remote. Does not delete local branch.

`git pull <remote> <branch>` - Fetch updates and automatically merge them into the branch. Without any arguments it pulls into current branch from its upstream.

## Undoing changes

`git revert <commit-hash>` - Create new commit that return state to the old snapshot.

`git reset [--soft] [--hard] <commit-hash>` - Discard all commits until the given one.
- `--soft`: All changes after that commit stay in the working directory.
- `--hard`: Delete all changes until that commit permanently.