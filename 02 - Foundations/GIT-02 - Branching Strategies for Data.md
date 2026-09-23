---
id: GIT-02
title: Branching Strategies for Data
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - GIT-02
---

# GIT-02 - Branching Strategies for Data

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Manage features, bug fixes, and data schema migrations across distributed teams using trunk-based flows.

## Concepts
- **Trunk-Based Development vs GitFlow**: Short-lived feature branches (< 1–2 days) merged into `main`.
- **Fast-Forward vs Merge Commits**: `git merge --ff-only` vs merge commits.
- **Feature Flags in Pipelines**: Decoupling code deployment from feature release.
- **Branch Naming Conventions**: Standardized branch prefixes.

## Learning Resource
- **Title**: Pro Git (2nd Edition) - Chapter 3: Git Branching
- **Provider / Author**: Scott Chacon & Ben Straub
- **URL**: https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows
- **Type**: Free Official Book
- **Topic**: Branching Workflows, Trunk-Based Development
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a feature branch `feat/add-parquet-extractor`.
- [ ] Make 2 commits, open a pull request, and configure squash-and-merge.
- [ ] Sync local main cleanly via `git pull --rebase origin main`.

## Completion Criteria
- [ ] Explain why trunk-based development is preferred in data engineering.
- [ ] Configure git to default to rebase on pull.
- [ ] Safely delete local and remote branches after merging.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Git (macOS) | Version control | Yes (Native) | Yes | `Built-in` | https://git-scm.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Configuration
```bash
git config --global pull.rebase true
```

## Related Lessons
- Prerequisites: [[GIT-01 - Git Internals and Staging]]
- Next Lesson: [[GIT-03 - Conflict Resolution and Rebasing]]
- Phase Overview: [[Phase 1 - Foundations]]
