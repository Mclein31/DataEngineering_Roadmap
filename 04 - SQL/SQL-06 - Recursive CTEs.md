---
id: SQL-06
title: Recursive CTEs
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-06
---

# SQL-06 - Recursive CTEs

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Traverse tree structures, organizational hierarchies, and bill-of-materials graphs using recursive SQL CTEs.

## Concepts
- **Recursive CTE Architecture (`WITH RECURSIVE`)**:
  - **Anchor Member**: Base query returning initial seed rows.
  - `UNION ALL`: Combining anchor with recursive iterations.
  - **Recursive Member**: Query referencing the CTE itself, executing iteratively until returning an empty set.
- **Recursion Termination**: Termination conditions preventing infinite loops.
- **Tracking Traversal Depth**: Incrementing a `depth` or `level` counter and constructing path breadcrumbs.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Recursive Queries
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/queries-with.html#QUERIES-WITH-RECURSIVE
- **Type**: Official Documentation
- **Topic**: Recursive SQL, Hierarchies, Trees
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create an `employees` table with `emp_id`, `emp_name`, and `manager_id`.
- [ ] Write a recursive CTE that queries the organizational hierarchy, displaying each employee's reporting level and full management path.
- [ ] Write a recursive CTE generating a sequence of dates between two bounds without `generate_series()`.

## Completion Criteria
- [ ] Write a recursive CTE traversing an organizational chart to find all direct and indirect reports.
- [ ] Implement cycle prevention to protect against circular manager references.
- [ ] Generate a date dimension sequence using recursive SQL.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Relational testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### Organizational Hierarchy Traversal
```sql
WITH RECURSIVE org_chart AS (
    -- Anchor Member: Top-level CEO (manager_id IS NULL)
    SELECT emp_id, emp_name, manager_id, 1 as hierarchy_level, emp_name::TEXT as management_path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive Member: Join employees to their managers
    SELECT e.emp_id, e.emp_name, e.manager_id, o.hierarchy_level + 1, o.management_path || ' -> ' || e.emp_name
    FROM employees e
    JOIN org_chart o ON e.manager_id = o.emp_id
)
SELECT * FROM org_chart ORDER BY hierarchy_level, emp_name;
```

## Related Lessons
- Prerequisites: [[SQL-05 - Subqueries and CTEs]]
- Next Lesson: [[SQL-07 - Window Functions Ranking]]
- Phase Overview: [[Phase 1 - Foundations]]
