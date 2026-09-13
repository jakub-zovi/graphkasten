---
tags:
  - cs
  - cs/swe
created: 2025-10-02T10:01
modified: 2025-10-02T10:11
published:
sources:
  - "[Merging vs. rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)"
topics:
  - Git
  - Merge
  - Rebase
  - Version Control
authors:
ai-assisted:
hidden:
public: true
---
# Merging vs rebasing
The first thing to understand about `git rebase` is that it solves the same problem as `git merge`. Both of these commands are designed to integrate changes from one branch into another branch—they just do it in very different ways.
## Merge
The easiest option is to merge the `main` branch into the feature branch using something like the following:

```css
git checkout feature
git merge main
```

Or, you can condense this to a one-liner:

```css
git merge feature main
```

This creates a new “merge commit” in the `feature` branch that ties together the histories of both branches, giving you a branch structure that looks like this:

![Merging main into feature branch](https://wac-cdn.atlassian.com/dam/jcr:4639eeb8-e417-434a-a3f8-a972277fc66a/02%20Merging%20main%20into%20the%20feature%20branh.svg?cdnVersion=3003)

Merging is nice because it’s a _non-destructive_ operation ([[Merging Is Non-Destructive]]). The existing branches are not changed in any way. This avoids all of the potential pitfalls of rebasing (discussed below).

==On the other hand, this also means that the `feature` branch will have an extraneous merge commit every time you need to incorporate upstream changes. If `main` is very active, this can pollute your feature branch’s history quite a bit.== While it’s possible to mitigate this issue with advanced `git log` options, it can make it hard for other developers to understand the history of the project.
## Rebase
As an alternative to merging, you can rebase the `feature` branch onto `main` branch using the following commands:

```css
git checkout feature
git rebase main
```

This moves the entire `feature` branch to begin on the tip of the `main` branch, effectively incorporating all of the new commits in `main`. But, instead of using a merge commit, rebasing _re-writes_ the project history by creating brand new commits for each commit in the original branch.

![Rebasing feature branch into main](https://wac-cdn.atlassian.com/dam/jcr:3bafddf5-fd55-4320-9310-3d28f4fca3af/03%20Rebasing%20the%20feature%20branch%20into%20main.svg?cdnVersion=3003)

The major benefit of rebasing is that you get a much cleaner project history ([[Cleaner History With Rebase]]). First, it eliminates the unnecessary merge commits required by `git merge`. Second, as you can see in the above diagram, rebasing also results in a perfectly linear project history—you can follow the tip of `feature` all the way to the beginning of the project without any forks. This makes it easier to navigate your project with commands like `git log`, `git bisect`, and `gitk`.

But, there are two trade-offs for this pristine commit history: safety and traceability. If you don’t follow the [Golden Rule of Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing), ==re-writing project history can be potentially catastrophic for your collaboration workflow==. And, less importantly, rebasing loses the context provided by a merge commit—you can’t see when upstream changes were incorporated into the feature.
## Golden Rule of Rebasing
==Once you understand what rebasing is, the most important thing to learn is when _not_ to do it. The golden rule of `git rebase` is to never use it on _public_ branches ([[Never Rebase On Public Branch]]).==

For example, think about what would happen if you rebased `main` onto your `feature` branch:

![Rebasing the main branch](https://wac-cdn.atlassian.com/dam/jcr:2908e0e6-f74b-4425-b5d2-f5eca8cfcd99/05%20Rebasing%20the%20main%20branch.svg?cdnVersion=3003)

The rebase moves all of the commits in `main` onto the tip of `feature`. The problem is that this only happened in _your_ repository. All of the other developers are still working with the original `main`. Since rebasing results in brand new commits, Git will think that your `main` branch’s history has diverged from everybody else’s.