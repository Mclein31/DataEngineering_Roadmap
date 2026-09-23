---
title: Weekly Study System
aliases:
  - Weekly Study System
---

# ⚙️ Repeatable Weekly Operating System

Designed for independent learners with 10–15 hours per week (1–2 hrs/day weekdays, 3.5 hrs Saturday deep work, 1.5 hrs Sunday sprint retro) on macOS.

---

## 📅 Day-by-Day Execution Cadence

### 🟢 Monday: New Concept Acquisition
- **Allocation**: 1.5 Hours
- **Primary Focus**: First principles learning and conceptual foundations.
- **Key Activities**:
  - Read the assigned lesson's Essential Resource (🔥).
  - Take structured notes directly inside the lesson file in the Obsidian vault.
  - Record 3 core technical mechanisms in [[Daily Log]].

### 🔵 Tuesday: Guided Code-Along
- **Allocation**: 1.5 Hours
- **Primary Focus**: Syntax execution and failure testing.
- **Key Activities**:
  - Replicate the lesson's code-along snippet in the local macOS terminal.
  - Test failure conditions by intentionally supplying invalid inputs or dropping dependencies.
  - Verify syntax execution and resolve any environment errors.

### 🟠 Wednesday: Independent Practice & Exercises
- **Allocation**: 2.0 Hours
- **Primary Focus**: Problem-solving without crutches.
- **Key Activities**:
  - Execute the lesson's Practical Terminal & Coding Challenge without referencing documentation.
  - Solve 2–3 targeted practice problems on DataLemur, LeetCode, or local sandbox.
  - Document any runtime bugs or edge-case discoveries in [[Daily Log]].

### 🟣 Thursday: Second Concept Acquisition & Expansion
- **Allocation**: 1.5 Hours
- **Primary Focus**: Deepening scope and connecting architectural layers.
- **Key Activities**:
  - Read the second assigned lesson of the week or dive into the Recommended Resource (⭐).
  - Connect the new concept to prior lessons using bidirectional Obsidian `[[wikilinks]]`.
  - Complete the Definition of Done checklist for the lesson note.

### 🟡 Friday: Synthesis & Code Review
- **Allocation**: 1.5 Hours
- **Primary Focus**: Software engineering rigor and refactoring.
- **Key Activities**:
  - Run linting (`ruff`) and static analysis (`mypy --strict`) over all code written during the week.
  - Refactor messy procedural scripts into typed, reusable functions or classes.
  - Prepare the local environment and tasks for the weekend project block.

### 🔴 Saturday: Deep Project Work Block
- **Allocation**: 3.5 Hours
- **Primary Focus**: Uninterrupted engineering implementation.
- **Key Activities**:
  - Dedicated implementation block on the active monthly portfolio project.
  - Write modular pipeline components, configure Docker Compose services, or build dbt models.
  - Commit all working code to GitHub following conventional commit standards.

### ⚪ Sunday: Sprint Retrospective & Weekly Review
- **Allocation**: 1.5 Hours
- **Primary Focus**: Reflection, self-auditing, and schedule calibration.
- **Key Activities**:
  - Complete [[Weekly Review]] (log hours, audit blockers, review sprint goals).
  - Update the self-assessment scoring in [[Skill Matrix]].
  - Review upcoming sprint commitments and configure tasks for the following week.

---

## 🧘 Habit & Focus Guidelines
1. **Zero Context Switching**: Turn off notifications during the 90-minute weekday blocks.
2. **Terminal First**: Always execute commands manually rather than relying on GUI clicks.
3. **Debug Without Copy-Paste**: Read error tracebacks from bottom to top before searching.
4. **Log Everything**: If you fixed an issue, record it in [[Daily Log]] so you never debug the same issue twice.
