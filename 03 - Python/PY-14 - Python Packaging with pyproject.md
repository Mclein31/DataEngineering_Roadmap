---
id: PY-14
title: Python Packaging with pyproject.md
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-14
---

# PY-14 - Python Packaging with pyproject.md

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Package data pipeline utilities and CLI tools into installable, versioned Python libraries conforming to pyproject.toml.

## Concepts
- **PEP 621 Standard**: Standardizing project metadata in `pyproject.toml` (`[project]`, `name`, `version`, `dependencies`).
- **Build Backends**: `hatchling`, `flit`, `setuptools`.
- **CLI Entry Points (`[project.scripts]`)**: Exposing Python functions as global executable terminal commands.
- **Editable Installs (`uv pip install -e .`)**: Developing package modules with immediate reflection of code changes.

## Learning Resource
- **Title**: Python Packaging User Guide
- **Provider / Author**: Python Packaging Authority (PyPA)
- **URL**: https://packaging.python.org/en/latest/
- **Type**: Official Guide
- **Topic**: Python Packaging, CLI Tools, pyproject.toml
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Structure your project code into a package directory `src/pipeline_toolkit`.
- [ ] Configure `pyproject.toml` with `[build-system]` using `hatchling` and define a CLI entry point:
  `pipeline-cli = "pipeline_toolkit.cli:main"`.
- [ ] Install in editable mode: `uv pip install -e .` and verify executing `pipeline-cli --help` from any terminal path.

## Completion Criteria
- [ ] Successfully install custom data package locally via `uv pip install -e .`.
- [ ] Execute the custom CLI command directly from the macOS terminal.
- [ ] Build a distribution wheel (`.whl`) using `uv build`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| uv / hatchling | Packaging and build backend | Yes (Native) | Yes | `uv add --build hatchling` | https://docs.astral.sh/uv/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### pyproject.toml CLI Entry Point
```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "de-toolkit"
version = "0.1.0"
dependencies = ["httpx", "polars", "pydantic"]

[project.scripts]
de-extract = "de_toolkit.cli:run_extraction"
```

## Related Lessons
- Prerequisites: [[PY-13 - Unit Testing with pytest]]
- Next Lesson: [[SQL-01 - Relational Execution Order]]
- Phase Overview: [[Phase 1 - Foundations]]
