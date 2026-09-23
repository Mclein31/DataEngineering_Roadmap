---
id: LNX-01
title: Shell Navigation and Permissions
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-01
---

# LNX-01 - Shell Navigation and Permissions

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master POSIX terminal navigation, file ownership/permissions, and process monitoring in macOS Zsh/Bash environments.

## Concepts
- **macOS Shell Environment (Zsh & Bash)**:
  - macOS has used **Zsh** (`/bin/zsh`) as the default login shell since macOS Catalina (10.15). User environment variables and aliases are stored in `~/.zshrc`.
  - Scripts utilizing `#!/usr/bin/env bash` execute seamlessly via the built-in macOS Bash runtime (`/bin/bash`).
- **POSIX File Permissions Bitmask**: Understanding octal representation (`4=Read`, `2=Write`, `1=Execute`) across User (u), Group (g), and Others (o). Calculating permissions like `755` (`rwxr-xr-x`) vs `644` (`rw-r--r--`). Identical behavior across macOS and Linux.
- **File Ownership (`chown`, `chgrp`)**: How the Unix kernel validates access rights against UID and GID metadata stored inside filesystem inodes.
- **macOS Process Lifecycle & Signal Handling**: Process IDs (PIDs), Parent Process IDs (PPIDs), `ps aux`, `top`, and sending kernel signals via `kill`:
  - `SIGTERM (15)`: Requests graceful termination, allowing application to clean up resources, close database sockets, and flush buffers.
  - `SIGKILL (9)`: Immediate kernel-level process destruction; cannot be trapped or ignored.
  - *macOS Tip*: You can also inspect process resource consumption visually using macOS **Activity Monitor** (`open -a "Activity Monitor"`).
- **Job Control**: Running jobs in the background (`&`), listing active session jobs (`jobs -l`), and moving tasks between background and foreground (`bg`, `fg`).

## Learning Resource
- **Title**: Linux Journey (Permissions & Process Management)
- **Provider / Author**: Linux Journey Community
- **URL**: https://linuxjourney.com/
- **Type**: Interactive Tutorial
- **Topic**: CLI Navigation, Permissions, Processes
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a shell script `monitor.sh`, inspect permissions with `ls -la`, and update permissions to `750` using `chmod`.
- [ ] Launch a continuous background Python loop in the terminal: `python3 -c "import time; [time.sleep(1) for _ in iter(int, 1)]" &`.
- [ ] Locate the process PID using `ps aux | grep python3`, verify its state, and terminate it gracefully using `kill -15 <PID>`.

## Completion Criteria
- [ ] Explain the exact difference between `chmod 644` and `chmod 755` without checking documentation.
- [ ] Launch, background, foreground, and terminate a running process using its PID via the terminal.
- [ ] Inspect file inode and permission metadata using `stat` or `ls -la`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| macOS Terminal (Zsh/Bash) | POSIX command-line interaction | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| iTerm2 | Enhanced terminal emulator for macOS | Yes | Yes | Install via `brew install --cask iterm2` |

## Notes
### Octal Permission Breakdown
```text
Value   Binary   Permission
  7      111     rwx (Read, Write, Execute)
  6      110     rw- (Read, Write)
  5      101     r-x (Read, Execute)
  4      100     r-- (Read only)
  0      000     --- (No permissions)
```

## Related Lessons
- Prerequisites: None
- Next Lesson: [[LNX-02 - Standard Streams and Pipelines]]
- Phase Overview: [[Phase 1 - Foundations]]
