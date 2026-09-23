---
id: MOD-07
title: Data Vault 2 Basics
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-07
---

# MOD-07 - Data Vault 2 Basics

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Data Vault 2.0 modeling architecture: Hubs, Links, and Satellites for agile enterprise data integration.

## Concepts
- **Data Vault 2.0 Philosophy**: Designed for enterprise scalability, resilience to source system changes, and parallel loading.
- **Core Entities**:
  - **Hubs**: Unique list of business keys (`customer_number`, `order_number`) with cryptographic hash keys (MD5 or SHA-256) and load timestamps. No descriptive data.
  - **Links**: Represents transactions or relationships between Hubs (e.g., `Customer-Order-Product`).
  - **Satellites**: Descriptive context and point-in-time attributes attached to Hubs or Links. Allows parallel loading of context from disparate source systems.
- **Hash Keys vs Auto-Incrementing Keys**: Using deterministic SHA-256 hashes of natural keys to allow distributed workers to generate keys independently without coordination.

## Learning Resource
- **Title**: Building a Scalable Data Warehouse with Data Vault 2.0
- **Provider / Author**: Dan Linstedt & Michael Olschimke
- **URL**: https://www.sciencedirect.com/book/9780128025109/building-a-scalable-data-warehouse-with-data-vault-20
- **Type**: Textbook
- **Topic**: Data Vault 2.0, Hubs, Links, Satellites
- **Difficulty**: Advanced
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Model a retail order system using Data Vault: create `hub_customer`, `hub_order`, `link_customer_order`, and `sat_customer_details`.
- [ ] Write SQL demonstrating how a source column deletion affects only a Satellite table, leaving Hubs and Links intact.

## Completion Criteria
- [ ] Explain the roles of Hubs, Links, and Satellites.
- [ ] Calculate deterministic hash keys using SHA-256 in SQL.
- [ ] Articulate why Data Vault is preferred for enterprise environments with constantly changing source systems.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 (via Docker) | Relational database testing | Yes (Docker) | Yes | `docker run -d -p 5432:5432 postgres:16` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Data Vault Structure
```text
[Hub: Customer] <==== [Link: Cust_Order] ====> [Hub: Order]
       ║                                             ║
[Sat: Cust_Profile]                           [Sat: Order_Details]
```

## Related Lessons
- Prerequisites: [[MOD-01 - Relational Normalization 1NF to 3NF]]
- Next Lesson: [[MOD-08 - One Big Table vs Star Schema]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
