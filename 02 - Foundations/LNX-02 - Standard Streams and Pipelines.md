---
id: LNX-02
title: Standard Streams and Pipelines
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-02
---

# LNX-02 - Standard Streams and Pipelines

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Chain utilities using Unix streams to inspect, filter, and manipulate data streams without loading entire files into memory.

## Concepts
- **Standard POSIX Streams & File Descriptors**: `stdin (FD 0)`, `stdout (FD 1)`, `stderr (FD 2)`.
- **Redirection Mechanics**: Overwriting (`>`), appending (`>>`), redirecting stderr (`2>`), combining stdout and stderr (`2>&1`).
- **Unix Pipelines (`|`)**: Inter-process communication using anonymous in-memory FIFO buffers where stdout of upstream becomes stdin of downstream.
- **Tee Utility (`tee`)**: Splitting a stream to simultaneously write to disk and forward to downstream stdout.

## Learning Resource
- **Title**: Linux Journey (Text and Streams)
- **Provider / Author**: Linux Journey Community
- **URL**: https://linuxjourney.com/
- **Type**: Interactive Tutorial
- **Topic**: POSIX Streams, Redirection, Piping
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Execute a command that generates both standard output and an intentional error; redirect stdout to `output.log` and stderr to `error.log`.
- [ ] Use a single pipeline to generate 1,000 numbers, filter for even numbers, write raw results to `evens.txt` using `tee`, and count total lines using `wc -l`.
- [ ] Suppress error output from a noisy terminal scan by redirecting stderr to `/dev/null`.

## Completion Criteria
- [ ] Successfully isolate `stderr` from `stdout` in a single shell command line.
- [ ] Chain at least 3 utilities using pipes to transform raw stream data without writing intermediate files.
- [ ] Explain why writing intermediate files to disk degrades pipeline performance compared to Unix pipes.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| macOS Terminal (Zsh/Bash) | Stream execution and redirection | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Stream Redirection Cheat Sheet
```bash
# Redirect stdout only
python3 pipeline.py > output.log

# Redirect stderr only
python3 pipeline.py 2> errors.log

# Merge stderr into stdout and pipe to downstream parser
python3 pipeline.py 2>&1 | grep "CRITICAL"
```

## Related Lessons
- Prerequisites: [[LNX-01 - Shell Navigation and Permissions]]
- Next Lesson: [[LNX-03 - Text Wrangling with grep sed awk]]
- Phase Overview: [[Phase 1 - Foundations]]
