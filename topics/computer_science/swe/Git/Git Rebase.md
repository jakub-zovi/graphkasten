---
tags:
  - cs
  - cs/swe
created: 2026-03-15T00:00
modified:
published:
sources:
  - "[git-rebase docs](https://git-scm.com/docs/git-rebase)"
  - "[Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)"
topics:
  - Git
  - Rebase
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Git Rebase
- [git-scm.com/docs/git-rebase](https://git-scm.com/docs/git-rebase)
> Rebasing re-applies commits on top of another base, rewriting history to produce a linear commit graph. See also [[Merging vs rebasing]] for a conceptual comparison with merging.
## Commands
### Basic Rebase
```bash
git rebase <base>                                    # rebase current branch onto <base>
git rebase main feature                              # rebase feature onto main (no checkout needed)
git rebase --onto <newbase> <upstream> <branch>      # transplant <branch> onto <newbase>
```
### Interactive Rebase
```bash
git rebase -i HEAD~<n>             # interactively edit last n commits
git rebase -i <commit-hash>        # interactively edit commits after <commit-hash>
```
Interactive actions available per commit:
- `pick` — keep commit as-is
- `reword` — keep commit, edit message
- `edit` — pause to amend the commit
- `squash` — meld into previous commit, combine messages
- `fixup` — meld into previous commit, discard message
- `drop` — remove commit entirely
- `exec` — run a shell command after the commit
### Conflict Resolution
```bash
git rebase --continue              # after resolving conflicts, continue
git rebase --skip                  # skip the current conflicting commit
git rebase --abort                 # abort and return to pre-rebase state
```
### Autosquash
```bash
git commit --fixup=<commit>        # mark commit as fixup for <commit>
git commit --squash=<commit>       # mark commit as squash for <commit>
git rebase -i --autosquash HEAD~n  # auto-arrange fixup!/squash! commits
```
## Notes
- Never rebase public/shared branches — rewrites history and diverges others' copies ([[Merging vs rebasing]])
- `--onto` is useful for moving a stack of commits to a completely different base
- Interactive rebase is the primary tool for cleaning up local commit history before a PR
