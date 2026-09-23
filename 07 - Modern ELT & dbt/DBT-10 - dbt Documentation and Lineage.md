---
id: DBT-10
title: dbt Documentation and Lineage
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-10
---

# DBT-10 - dbt Documentation and Lineage

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Generate interactive documentation and visual lineage graphs to communicate pipeline data provenance across engineering teams.

## Concepts
- **Self-Documenting Pipelines**: Documenting models, columns, and assumptions directly in `schema.yml` using descriptions and markdown doc blocks (`{% docs %}`).
- **Interactive Lineage Graph (DAG)**: Visualizing data flow from raw sources through staging, intermediate, and marts.
- **dbt Docs Compilation**: `dbt docs generate` compiling manifest, catalog, and index artifacts into static web assets.
- **Serving Documentation**: Running `dbt docs serve` to explore column lineage, data types, and model dependencies locally.

## Learning Resource
- **Title**: dbt Documentation Guide
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/collaborate/documentation
- **Type**: Official Documentation
- **Topic**: Documentation, Lineage Graphs, DAGs
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Add comprehensive column-level descriptions across all models in `schema.yml`.
- [ ] Create a Markdown doc block `docs/customer_status.md` explaining customer lifecycle statuses.
- [ ] Generate and launch local documentation website using `dbt docs generate && dbt docs serve`.

## Completion Criteria
- [ ] Generate a complete dbt documentation site locally.
- [ ] Inspect the visual DAG lineage graph and trace an individual column from source to mart.
- [ ] Embed reusable markdown doc blocks into model documentation.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Documentation generation | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Markdown Doc Block Example
```markdown
{% docs order_status_description %}
The current operational state of the order:
- `PENDING`: Placed by customer, awaiting credit card authorization.
- `COMPLETED`: Funds captured and physical order dispatched.
- `REFUNDED`: Full transaction amount reversed to customer.
{% enddocs %}
```

## Related Lessons
- Prerequisites: [[DBT-07 - dbt Testing Framework]]
- Next Lesson: [[DW-01 - Cloud Warehouse Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
