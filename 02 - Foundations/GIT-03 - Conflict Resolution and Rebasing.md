---
id: GIT-03
title: Conflict Resolution and Rebasing
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - GIT-03
---

# GIT-03 - Conflict Resolution and Rebasing

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Maintain linear, legible commit histories and resolve merge conflicts cleanly using interactive rebasing.

## Concepts
- **Interactive Rebasing (`git rebase -i <base>`)**: Rewriting local unpushed history.
- **Rebase vs Merge Mechanics**: Moving branch base to maintain linear history.
- **Conflict Markers**: Navigating `<<<<<<< HEAD` markers.
- **Rebase Recovery**: `git rebase --abort` and `git reflog`.

## Learning Resource
- **Title**: Pro Git (2nd Edition) - Rewriting History
- **Provider / Author**: Scott Chacon & Ben Straub
- **URL**: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
- **Type**: Free Official Book
- **Topic**: Interactive Rebasing, Squash, Fixup
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a feature branch with 4 messy commits.
- [ ] Execute `git rebase -i HEAD~4` to squash into a single commit.
- [ ] Intentionally cause a merge conflict, resolve markers, and complete rebase.

## Completion Criteria
- [ ] Clean up a branch with 5 messy commits into a single commit.
- [ ] Resolve a merge conflict cleanly without dropping code.
- [ ] Recover a lost commit using `git reflog`.

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
### Rebase Commands
```text
pick, reword, edit, squash, fixup, drop
```

## Related Lessons
- Prerequisites: [[GIT-02 - Branching Strategies for Data]]
- Next Lesson: [[GIT-04 - Semantic Versioning]]
- Phase Overview: [[Phase 1 - Foundations]]
