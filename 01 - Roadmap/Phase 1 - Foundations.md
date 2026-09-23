---
title: Phase 1 - Systems & Programming Foundations
phase: Phase 1
duration: Months 1–3 (12 Weeks)
aliases:
  - Phase 1
  - Phase 1 - Foundations
---

# 💻 Phase 1: Systems & Programming Foundations

## Overview
Phase 1 establishes the rock-solid software engineering foundations required for modern Data Engineering. Rather than jumping directly into high-level cloud abstractions or massive distributed engines, Phase 1 ensures you master the POSIX terminal, low-level process management, linear Git history, production-grade typed Python 3.12+, in-memory columnar data manipulation with Polars, and deep analytical SQL.

---

## 🎯 Target Capabilities
- Master POSIX command-line navigation, standard Unix streams (`stdin`, `stdout`, `stderr`), pipes, and background process control.
- Parse and wrangle multi-gigabyte log files directly in the terminal using `grep`, `sed`, `awk`, and `cut`.
- Write automated, resilient Bash scripts adhering to `set -euo pipefail` with deterministic error traps and exit codes.
- Manage Git repositories with linear commit histories using interactive rebasing (`git rebase -i`), trunk-based flows, and Conventional Commits.
- Write modular, idiomatic Python 3.12+ enforcing strict static typing via `mypy --strict` with zero runtime type surprises.
- Enforce rigid data schemas on untyped incoming API and file payloads using Pydantic v2 validation models.
- Stream multi-gigabyte datasets with <50MB RAM footprints using memory-efficient custom Python generators.
- Vectorize single-node analytical transformations using Polars LazyFrames and Apache Arrow zero-copy memory representation.
- Build automated, deterministic unit test suites with `pytest`, fixtures, and mocks maintaining $\ge 85\%$ test coverage.
- Write complex analytical SQL queries utilizing logical execution order, anti-joins, recursive CTEs, and explicit window frames (`ROWS BETWEEN`).

---

## 📚 Modules in Phase 1
- **Module 02: Systems Foundations (macOS POSIX & Git)**
  - [[LNX-01 - Shell Navigation and Permissions]]
  - [[LNX-02 - Standard Streams and Pipelines]]
  - [[LNX-03 - Text Wrangling with grep sed awk]]
  - [[LNX-04 - Production Bash Scripting]]
  - [[LNX-05 - Cron Scheduling and Automation]]
  - [[LNX-06 - Networking Fundamentals for DE]]
  - [[GIT-01 - Git Internals and Staging]]
  - [[GIT-02 - Branching Strategies for Data]]
  - [[GIT-03 - Conflict Resolution and Rebasing]]
  - [[GIT-04 - Semantic Versioning]]
- **Module 03: Production Python & Software Engineering**
  - [[PY-01 - Python Internals and uv]]
  - [[PY-02 - Strict Type Hinting and mypy]]
  - [[PY-03 - Data Validation with Pydantic]]
  - [[PY-04 - Functional Mechanics and Itertools]]
  - [[PY-05 - Memory Optimization with Generators]]
  - [[PY-06 - Advanced OOP and Protocols]]
  - [[PY-07 - Metaprogramming with Decorators]]
  - [[PY-08 - Context Managers]]
  - [[PY-09 - Structured Logging]]
  - [[PY-10 - Resilient HTTP Ingestion with httpx]]
  - [[PY-11 - Vectorized Processing with Polars]]
  - [[PY-12 - Columnar Serialization with PyArrow]]
  - [[PY-13 - Unit Testing with pytest]]
  - [[PY-14 - Python Packaging with pyproject]]
- **Module 04: Advanced SQL & Query Optimization**
  - [[SQL-01 - Relational Execution Order]]
  - [[SQL-02 - Filtering and Three-Valued Logic]]
  - [[SQL-03 - Relational Joins and Anti-Joins]]
  - [[SQL-04 - Advanced Grouping Sets and Rollups]]
  - [[SQL-05 - Subqueries and CTEs]]
  - [[SQL-06 - Recursive CTEs]]
  - [[SQL-07 - Window Functions Ranking]]
  - [[SQL-08 - Window Functions Value Navigation]]
  - [[SQL-09 - Window Functions Frame Specifications]]
  - [[SQL-10 - Pivot and Conditional Aggregation]]
  - [[SQL-11 - Execution Plans with EXPLAIN]]
  - [[SQL-12 - Relational Access Methods]]
  - [[SQL-13 - Join Algorithms]]
  - [[SQL-14 - Indexing Strategies and B-Trees]]

---

## 🏆 Milestone Gate 1 Exit Criteria
- [ ] Pass timed 60-minute SQL test on joins, anti-joins, recursive CTEs, and explicit window frames.
- [ ] Deliver a production-grade Python CLI data extraction tool with `mypy --strict` compliance and $\ge 85\%$ test coverage via `pytest-cov`.
- [ ] Successfully rebase a 5-commit divergent feature branch into a clean conventional commit history.
