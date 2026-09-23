---
id: LNX-04
title: Production Bash Scripting
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-04
---

# LNX-04 - Production Bash Scripting

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Write automated, fault-tolerant shell scripts for file movement, validation, and pipeline triggering with robust error traps.

## Concepts
- **The Strict Mode Shebang**: `#!/usr/bin/env bash` and `set -euo pipefail`.
- **Trap Mechanism**: Intercepting signals and abnormal exits (`trap 'cleanup' EXIT ERR SIGINT`).
- **Positional Arguments & Option Parsing**: Validating `$#`, `$1`, `${1:-default}`, shift loops.
- **Exit Status Codes (`$?`)**: Standard POSIX exit conventions.

## Learning Resource
- **Title**: Bash Guide for Beginners
- **Provider / Author**: Machtelt Garrels / The Linux Documentation Project
- **URL**: https://tldp.org/LDP/Bash-Beginners-Guide/html/
- **Type**: Free Web Guide
- **Topic**: Bash Automation, Error Trapping
- **Difficulty**: Intermediate
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Write a production script `archive_logs.sh` that takes a directory path as argument `$1`.
- [ ] Enforce `set -euo pipefail` and validate that `$1` is provided; exit with code 1 and error message if missing.
- [ ] Implement a `trap` that cleans up temporary scratch files even if killed via `SIGINT`.

## Completion Criteria
- [ ] Explain why `set -euo pipefail` is mandatory in enterprise data ingestion scripts.
- [ ] Write a script that executes a cleanup function via `trap` upon encountering an error.
- [ ] Validate required arguments and return explicit non-zero exit codes upon failure.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Bash / Zsh (macOS) | Script execution | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Production Script Template
```bash
#!/usr/bin/env bash
set -euo pipefail
SCRATCH_DIR=$(mktemp -d)
trap 'rm -rf "${SCRATCH_DIR}"' EXIT ERR SIGINT
```

## Related Lessons
- Prerequisites: [[LNX-03 - Text Wrangling with grep sed awk]]
- Next Lesson: [[LNX-05 - Cron Scheduling and Automation]]
- Phase Overview: [[Phase 1 - Foundations]]
