---
tags:
  - cs
  - cs/swe
created: 2026-03-15T00:00
modified:
published:
sources:
  - "[Git Worktrees](https://git-scm.com/docs/git-worktree)"
topics:
  - Git
  - Worktrees
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Git Worktrees
- [git-scm.com/docs/git-worktree](https://git-scm.com/docs/git-worktree)
> A git worktree allows you to check out multiple branches simultaneously into separate directories, all sharing the same `.git` repository. This enables parallel work without stashing or switching branches.
## Use Cases
- Work on a hotfix while keeping your feature branch untouched
- Run tests on one branch while developing on another
- Review a PR in an isolated directory without context-switching
## Commands
### Create
```bash
git worktree add <path> <branch>          # check out existing branch into <path>
git worktree add <path> -b <new-branch>   # create new branch and check it out
git worktree add <path>                   # detached HEAD at current commit
```
### List & Inspect
```bash
git worktree list                         # show all worktrees with HEAD and branch
git worktree list --porcelain             # machine-readable output
```
### Remove
```bash
git worktree remove <path>                # remove worktree (must be clean)
git worktree remove --force <path>        # force-remove even with uncommitted changes
git worktree prune                        # clean up stale worktree metadata
```
### Move & Lock
```bash
git worktree move <path> <new-path>       # relocate a worktree
git worktree lock <path>                  # prevent pruning (e.g. on removable drive)
git worktree unlock <path>                # re-enable pruning
```
## Notes
- Each worktree has its own working directory and index but shares refs, objects, and config
- A branch can only be checked out in one worktree at a time
- `.git/worktrees/` stores per-worktree metadata
