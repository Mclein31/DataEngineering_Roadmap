---
id: LNX-05
title: Cron Scheduling and Automation
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-05
---

# LNX-05 - Cron Scheduling and Automation

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Automate local script execution on deterministic schedules using cron syntax and manage process scheduling constraints.

## Concepts
- **Cron Daemon Architecture & Syntax**: Five-field time specification: `m h dom mon dow`.
- **Environment Pitfalls in Cron**: Stripped `$PATH` and absent user dotfiles.
- **Absolute Binary Path Enforcement**: Specifying exact binary locations.
- **Log Redirection**: Appending cron job output and errors to timestamped log files.

## Learning Resource
- **Title**: Linux Journey (Automating Tasks with Cron)
- **Provider / Author**: Linux Journey Community
- **URL**: https://linuxjourney.com/
- **Type**: Interactive Tutorial
- **Topic**: crontab, task automation
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Inspect existing user crontab using `crontab -l`.
- [ ] Write a test script `heartbeat.sh` that appends the current timestamp to `~/heartbeat.log`.
- [ ] Schedule via `crontab -e` to execute every weekday at 06:00 AM.

## Completion Criteria
- [ ] Construct a valid cron expression for "Every 15 minutes between 9 AM and 5 PM on weekdays".
- [ ] Explain why full absolute binary paths must be used within cron jobs.
- [ ] Redirect both stdout and stderr of a cron job to a log file.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| crontab (macOS) | Job scheduler | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Crontab Entry Example
```bash
0 6 * * 1-5 /opt/homebrew/bin/uv run /Users/mclein/scripts/daily_etl.py >> /Users/mclein/logs/cron_etl.log 2>&1
```

### 🍎 macOS Cron Permissions & Native Daemon Architecture
1. **Full Disk Access Requirement**: On macOS (Sonoma & Sequoia), cron runs under `/usr/sbin/cron`. To allow cron to access your user directories and run scripts, you must grant permissions:
   - Open **System Settings > Privacy & Security > Full Disk Access**
   - Click `+`, press `Cmd + Shift + G`, enter `/usr/sbin/cron`, and enable it.
2. **macOS Native Daemons (`launchd`)**: While Linux distributions rely on `systemd` / `cron`, macOS natively uses `launchd` controlled via `launchctl` and Property List (`.plist`) files located in `~/Library/LaunchAgents/`.
3. **Why Data Engineers Learn Cron**: Despite `launchd` on macOS, cron syntax (`* * * * *`) is the **universal scheduling standard** across data engineering: it defines schedule intervals in **Apache Airflow**, **AWS EventBridge**, **Kubernetes CronJobs**, and **GCP Cloud Scheduler**.

## Related Lessons
- Prerequisites: [[LNX-04 - Production Bash Scripting]]
- Next Lesson: [[LNX-06 - Networking Fundamentals for DE]]
- Phase Overview: [[Phase 1 - Foundations]]
