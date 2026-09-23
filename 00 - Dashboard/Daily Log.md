---
title: Daily Study Log
aliases:
  - Daily Log
---

# 📝 Daily Study Log

Use this document to track your daily 1–2 hour learning blocks, record core technical mechanisms, log bugs, and maintain disciplined momentum.

---

## Daily Log Protocol
For each study session:
1. **Timestamp & Allocation**: Record date, start/end time, and total hours.
2. **Active Lesson**: Link the lesson note using `[[Lesson ID - Title]]`.
3. **Core Technical Mechanisms**: Record 3 concrete mechanisms learned (under-the-hood engine behavior, memory layouts, syntax nuances).
4. **Bugs & Gotchas Encountered**: Record terminal errors, unexpected behavior, and exact fix commands.
5. **Tomorrow's Commitment**: Explicitly specify the single next step.

---

## 📅 Log Entries

### Week 1 — Linux & Terminal Foundations

#### 2026-09-23 | Sprint Kickoff & Environment Setup
- **Time Allocated**: 1.5 Hours
- **Active Lesson**: [[LNX-01 - Shell Navigation and Permissions]]
- **3 Core Technical Mechanisms**:
  1. *File Permissions Bitmask*: POSIX permissions are evaluated as user, group, other using octal values (r=4, w=2, x=1). `chmod 750` assigns rwx to owner, rx to group, zero permissions to others.
  2. *Process Signals*: `kill -15` (SIGTERM) allows graceful teardown, closing file descriptors and database connections, whereas `kill -9` (SIGKILL) abruptly halts process execution at kernel level.
  3. *Background Job Control*: Appending `&` forks command to background; `fg` restores it to foreground; `jobs -l` displays background job PIDs.
- **Bugs & Gotchas Encountered**:
  - Script was initially missing execute permission (`zsh: permission denied: ./run.sh`). Resolved via `chmod +x ./run.sh`.
- **Tomorrow's Commitment**: Complete [[LNX-02 - Standard Streams and Pipelines]] and isolate stdout from stderr in a pipeline.

---

### 📋 Daily Entry Template (Copy & Paste for New Days)

```markdown
#### YYYY-MM-DD | [Lesson / Topic Title]
- **Time Allocated**: X.X Hours
- **Active Lesson**: `[[LESSON-ID - Title]]`
- **3 Core Technical Mechanisms**:
  1. 
  2. 
  3. 
- **Bugs & Gotchas Encountered**:
  - Issue: 
  - Resolution: 
- **Tomorrow's Commitment**: 
```
