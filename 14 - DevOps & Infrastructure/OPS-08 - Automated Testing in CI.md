---
id: OPS-08
title: Automated Testing in CI
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-08
---

# OPS-08 - Automated Testing in CI

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Integrate dbt schema testing and Terraform plan validation into automated CI/CD pull request pipelines.

## Concepts
- **dbt Testing in CI (Slim CI)**: Using `dbt test --select state:modified+` to test only models modified in a PR against an ephemeral test schema, saving 95% of CI warehouse compute.
- **Automated `terraform plan` on PR**: Generating an execution plan in CI and posting the plan summary as a pull request comment for team review.
- **Ephemeral Sandbox Environments**: Spinning up disposable DuckDB or LocalStack instances inside the GitHub Actions runner for zero-cost integration testing.

## Learning Resource
- **Title**: dbt Best Practices - Continuous Integration
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/best-practices/continuous-integration
- **Type**: Official Documentation
- **Topic**: Slim CI, dbt Testing in CI, Automated Verification
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Add a step to your GitHub Actions workflow running `dbt test` against an ephemeral DuckDB database.
- [ ] Add a Terraform validation step running `terraform fmt -check` and `terraform validate`.
- [ ] Verify that introducing an intentional SQL syntax error causes the CI runner to fail and block PR merge.

## Completion Criteria
- [ ] Execute automated dbt tests inside GitHub Actions CI.
- [ ] Validate Terraform configurations in CI before merging.
- [ ] Implement Slim CI concepts to test only modified data models.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| GitHub Actions | CI validation | Yes | Yes | `Web / GitHub` | https://github.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### dbt CI Step in GitHub Actions
```yaml
      - name: Run dbt Build and Tests
        run: |
          uv pip install dbt-core dbt-duckdb
          dbt build --project-dir dbt_project --profiles-dir dbt_project
```

## Related Lessons
- Prerequisites: [[OPS-07 - GitHub Actions CI-CD]], [[DBT-07 - dbt Testing Framework]]
- Next Lesson: [[DAT-01 - The 5 Pillars of Observability]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
