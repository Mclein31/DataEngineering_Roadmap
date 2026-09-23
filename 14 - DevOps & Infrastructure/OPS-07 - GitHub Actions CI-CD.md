---
id: OPS-07
title: GitHub Actions CI-CD
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-07
---

# OPS-07 - GitHub Actions CI-CD

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build automated Continuous Integration and Continuous Deployment (CI/CD) workflows using GitHub Actions to validate pipelines on every PR.

## Concepts
- **CI/CD for Data Engineering**: Automating code quality gating before merging into `main` (formatting, static analysis, unit tests, schema validation, infrastructure plans).
- **GitHub Actions Components**: Workflows (`.github/workflows/*.yml`), Triggers (`on: [push, pull_request]`), Jobs, Runners (Ubuntu/macOS), Steps.
- **Secret Management**: Storing cloud credentials and API keys in GitHub Repository Secrets (`${{ secrets.AWS_ACCESS_KEY_ID }}`).
- **CI Status Checks**: Blocking pull request merges if any linting or test step fails.

## Learning Resource
- **Title**: GitHub Actions Official Documentation
- **Provider / Author**: GitHub
- **URL**: https://docs.github.com/en/actions
- **Type**: Official Documentation
- **Topic**: CI/CD, GitHub Actions, Automated Testing
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a GitHub Actions workflow `.github/workflows/ci.yml`.
- [ ] Configure steps to checkout code, set up Python 3.12 with `uv`, run Ruff linter, and run Pytest test suite.
- [ ] Open a test pull request and observe automated checks running in real time.

## Completion Criteria
- [ ] Build a working GitHub Actions CI workflow triggered on Pull Requests.
- [ ] Configure automated linting and unit testing gating in CI.
- [ ] Enforce branch protection rules requiring passing CI checks before merging.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Git & GitHub | CI/CD execution | Yes | Yes | `Built-in / web` | https://github.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### GitHub Actions Workflow Example
```yaml
name: Data Pipeline CI

on:
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install uv and Python
        uses: astral-sh/setup-uv@v2
        with:
          python-version: "3.12"
      - name: Run Linter (Ruff)
        run: uv run ruff check .
      - name: Run Type Checker (mypy)
        run: uv run mypy --strict src/
      - name: Run Test Suite (pytest)
        run: uv run pytest tests/
```

## Related Lessons
- Prerequisites: [[GIT-02 - Branching Strategies for Data]], [[PY-13 - Unit Testing with pytest]]
- Next Lesson: [[OPS-08 - Automated Testing in CI]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
