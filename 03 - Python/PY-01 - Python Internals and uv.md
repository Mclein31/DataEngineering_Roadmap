---
id: PY-01
title: Python Internals and uv
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-01
---

# PY-01 - Python Internals and uv

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Set up fast, reproducible, isolated Python environments using modern tooling and understand CPython runtime execution.

## Concepts
- **CPython Runtime Mechanics**: Source code compilation to bytecode (`.pyc`), evaluation loop in the virtual machine, Global Interpreter Lock (GIL) memory model.
- **Astral `uv` Architecture**: Written in Rust, `uv` replaces `pip`, `pip-tools`, `virtualenv`, and `poetry` with 10–100x faster dependency resolution using global content-addressable wheel caching.
- **Modern Packaging with `pyproject.toml`**: The unified standard (PEP 517/518/621) replacing legacy `setup.py` and `requirements.txt`.
- **Lockfile Guarantees (`uv.lock`)**: Ensuring deterministic cross-environment builds across team members and CI/CD runners.

## Learning Resource
- **Title**: Python 3.12+ Official Documentation & uv Docs
- **Provider / Author**: Python Software Foundation / Astral
- **URL**: https://docs.astral.sh/uv/
- **Type**: Official Documentation
- **Topic**: Python Internals, Package Management
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install `uv` via Homebrew (`brew install uv`).
- [ ] Initialize a new project directory: `uv init data_pipeline && cd data_pipeline`.
- [ ] Pin Python 3.12, add dependencies (`uv add polars pydantic httpx`), inspect the generated `pyproject.toml` and `uv.lock`.
- [ ] Execute a test script inside the isolated environment using `uv run python main.py`.

## Completion Criteria
- [ ] Explain why `uv` achieves orders of magnitude faster resolution than `pip`.
- [ ] Run a Python script inside a pinned, isolated `uv` virtual environment without activating it globally.
- [ ] Inspect the structure of `pyproject.toml` and generate a frozen `uv.lock`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| uv | Python package resolver and virtualenv manager | Yes (Native) | Yes | `brew install uv` | https://docs.astral.sh/uv/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### uv Command Reference
```bash
# Initialize and manage
uv init my_pipeline
uv add polars pyarrow
uv lock
uv run python script.py
```

## Related Lessons
- Prerequisites: [[LNX-01 - Shell Navigation and Permissions]]
- Next Lesson: [[PY-02 - Strict Type Hinting and mypy]]
- Phase Overview: [[Phase 1 - Foundations]]
