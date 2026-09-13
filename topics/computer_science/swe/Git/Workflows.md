---
tags:
  - cs
  - cs/swe
created: 2024-10-03T14:16
modified: 2026-07-19T17:45
published:
sources:
topics:
  - Git Workflows
  - Feature Branching
  - Trunk-Based Development
  - Gitflow
  - Version Control
authors:
ai-assisted:
hidden:
public: true
---
# Workflows
## [[Feature Branching]] Git Workflow
- In this workflow, a **separate branch is created for each feature** being worked on. Developers work on their respective feature branches and only merge them into the main branch when the feature is complete.
![[feature_based.png]]
- Pros:
	- The main branch contains only finished and stable code.
	- Features can be developed and maintained independently without affecting the main branch.
- Cons:
	- Managing feature branches becomes challenging when multiple developers work on the same feature.
	- Longer branch lifespans can lead to complex merging conflicts.

## [[Trunk-based]] Development Git Workflow (Develop Branch)
- This workflow is similar to feature branching but introduces a **trunk (or develop) branch** that acts as an intermediary. New features are merged into the trunk branch first, which is then tested before merging to the main branch.

![[trunk_based.png]]

- Pros:
	- All features are tested together before merging into the main branch.
	- The main branch stays clean and stable.
	- Minor code changes can be made quickly without breaking the main branch.
- Cons:
	- Adds complexity to repository management with extra merging steps.
	- Developers need to resolve conflicts locally.
	- Requires regular updates to keep the main branch current.

## [[Gitflow]] Git Workflow
- This workflow builds upon the trunk-based workflow by adding two new branches: **Release** and **Hotfix**. The release branch is used for testing and bug fixes before a feature is merged into the main branch. The hotfix branch is used for emergency patches directly on the main branch.
- **This workflow is considered to be [legacy by Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).**

![[gitflow.png]]

- Pros:
	- Provides a structured way to test features before releasing.
	- Allows for swift, isolated fixes through hotfix branches.
- Cons:
	- Introduces more complexity with additional branches.
	- Requires strict discipline to manage release and hotfix branches effectively.