---
id: GIT-04
title: Semantic Versioning
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - GIT-04
---

# GIT-04 - Semantic Versioning

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce automated changelogs and deterministic release cycles on data repositories and pipeline packages.

## Concepts
- **Semantic Versioning Specification (SemVer 2.0.0)**: `MAJOR.MINOR.PATCH`.
- **Conventional Commits 1.0.0**: `feat:`, `fix:`, `refactor:`, `chore:`.
- **Breaking Change Notation**: `feat!:` or `BREAKING CHANGE:` footer.
- **Annotated Release Tags**: `git tag -a v1.2.0 -m "Release v1.2.0"`.

## Learning Resource
- **Title**: Conventional Commits Specification
- **Provider / Author**: Conventional Commits Working Group
- **URL**: https://www.conventionalcommits.org/en/v1.0.0/
- **Type**: Specification
- **Topic**: Commit conventions, changelogs
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Formulate 3 commits adhering to Conventional Commits.
- [ ] Tag the repository with an annotated tag `v1.0.0`.
- [ ] Determine how a required schema change impacts SemVer.

## Completion Criteria
- [ ] Correctly classify changes into MAJOR, MINOR, or PATCH.
- [ ] Write 5 consecutive conventional commits with structured footers.
- [ ] Create and inspect an annotated Git tag.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Git (macOS) | Tagging and releases | Yes (Native) | Yes | `Built-in` | https://git-scm.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Commit Format
```text
<type>[optional scope]: <description>
[optional body]
[optional footer(s)]
```

## Related Lessons
- Prerequisites: [[GIT-03 - Conflict Resolution and Rebasing]]
- Next Lesson: [[PY-01 - Python Internals and uv]]
- Phase Overview: [[Phase 1 - Foundations]]
