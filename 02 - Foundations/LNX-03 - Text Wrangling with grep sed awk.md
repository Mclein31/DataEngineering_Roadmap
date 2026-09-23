---
id: LNX-03
title: Text Wrangling with grep sed awk
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-03
---

# LNX-03 - Text Wrangling with grep sed awk

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Clean, filter, and parse delimited log and CSV files directly from the command line with zero RAM overhead.

## Concepts
- **Regular Expression Filtering with `grep`**: Extended regex (`-E`), inverting matches (`-v`), line counts (`-c`), case-insensitivity (`-i`).
- **Stream Editing with `sed`**: Global substitution pattern syntax (`s/pattern/replacement/g`), in-place file mutation (`-i`), deleting matching lines (`/pattern/d`).
- **Pattern Scanning & Processing with `awk`**: Field variables (`$1, $2, $NF`), record count (`NR`), field separators (`-F`), accumulating sums and averages.
- **Column Slicing with `cut`**: Delimited field selection (`cut -d',' -f1,3`).

## Learning Resource
- **Title**: Linux Journey (Text Wrangling)
- **Provider / Author**: Linux Journey Community
- **URL**: https://linuxjourney.com/
- **Type**: Interactive Tutorial
- **Topic**: sed, awk, grep, text manipulation
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Generate a synthetic 10,000-line web server access log.
- [ ] Filter out HTTP 200 codes, and print the top 5 requested IP addresses using `grep`, `awk`, and `sort`.
- [ ] Write an `awk` one-liner to parse a CSV and compute the average transaction amount of column 4.

## Completion Criteria
- [ ] Write an `awk` one-liner to sum a specific column in a CSV without loading the file into Python.
- [ ] Filter out commented (`#`) and empty lines from a configuration file using `grep -E -v '^#|^$'`.
- [ ] Replace all occurrences of a delimiter in a large file using `sed`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| awk, sed, grep (macOS) | Stream text parsing | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Production `awk` Patterns
```bash
# Calculate sum and average of column 3 in a comma-delimited file
awk -F',' '{sum += $3; count++} END {print "Sum:", sum, "Avg:", sum/count}' transactions.csv
```

### 🍎 Critical macOS vs Linux Syntax: `sed -i`
macOS includes the **BSD version** of `sed`, which requires an explicit backup extension argument when mutating files in-place:
```bash
# macOS (BSD sed) — In-place edit requires empty string '' for no backup:
sed -i '' 's/old_endpoint/new_endpoint/g' config.env

# Linux (GNU sed) — In-place edit takes no empty string:
sed -i 's/old_endpoint/new_endpoint/g' config.env
```
> [!TIP] GNU Tools on macOS
> If you wish to use standard GNU `sed` on macOS for identical behavior with Linux cloud runners, install via Homebrew:
> ```bash
> brew install gnu-sed
> # Invoked as `gsed` or symlinked to `sed`
> ```

## Related Lessons
- Prerequisites: [[LNX-02 - Standard Streams and Pipelines]]
- Next Lesson: [[LNX-04 - Production Bash Scripting]]
- Phase Overview: [[Phase 1 - Foundations]]
