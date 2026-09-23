---
id: GIT-01
title: Git Internals and Staging
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - GIT-01
---

# GIT-01 - Git Internals and Staging

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Git's low-level object model to debug history corruption, inspect blobs, and manage working states.

## Concepts
- **Git Object Storage (`.git/objects`)**: Blobs, Trees, Commits, Annotated Tags.
- **The Three Trees**: Working Directory, Staging Area (Index), and Commit History (`HEAD`).
- **Low-Level Plumbing Commands**: `git cat-file -p <hash>`, `git ls-tree <hash>`.

## Learning Resource
- **Title**: Pro Git (2nd Edition) - Chapter 10: Git Internals
- **Provider / Author**: Scott Chacon & Ben Straub
- **URL**: https://git-scm.com/book/en/v2/Git-Internals-Git-Objects
- **Type**: Free Official Book
- **Topic**: Git Object Models, SHA-1 Hashing
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Initialize a test git repo, stage a text file, and locate the newly generated blob in `.git/objects/`.
- [ ] Commit the file, use `git cat-file -p HEAD` to inspect the commit object, and locate the root tree hash.
- [ ] Demonstrate `git restore --staged <file>` vs `git restore <file>`.

## Completion Criteria
- [ ] Explain the relationship between blobs, trees, and commit objects.
- [ ] Inspect a commit object using `git cat-file -p <hash>`.
- [ ] Revert a dirty working directory without losing untracked files.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Git (macOS) | Version control | Yes (Native) | Yes | `Built-in / `brew install git`` | https://git-scm.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Git Object Commands
```bash
git cat-file -t <hash> # object type
git cat-file -p <hash> # content
```

## Related Lessons
- Prerequisites: [[LNX-01 - Shell Navigation and Permissions]]
- Next Lesson: [[GIT-02 - Branching Strategies for Data]]
- Phase Overview: [[Phase 1 - Foundations]]
