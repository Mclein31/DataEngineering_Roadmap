---
title: Curated Books & Official Literature
aliases:
  - Books and PDFs
---

# 📖 Curated Data Engineering Literature

The following textbooks represent the definitive foundational literature of modern distributed data systems. All references link to legitimate publisher platforms or free official author web editions.

---

## 📚 Essential Reading List

### 1. Designing Data-Intensive Applications (DDIA)
- **Author**: Martin Kleppmann
- **Publisher**: O'Reilly Media
- **Official URL**: [oreilly.com/library/view/designing-data-intensive-applications/9781491903117/](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/)
- **Core Topics**: Storage engines (B-Trees vs LSM-Trees), replication protocols, partitioning, transactions, consensus, stream processing.
- **Curriculum Integration**: [[DB-01 - Row vs Columnar Storage]], [[DB-02 - Write-Ahead Logging and Durability]], [[DES-01 - System Design Interview Framework]].

### 2. The Data Warehouse Toolkit (3rd Edition)
- **Authors**: Ralph Kimball & Margy Ross
- **Publisher**: John Wiley & Sons
- **Official URL**: [wiley.com](https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801)
- **Core Topics**: Dimensional modeling, Fact vs Dimension tables, Star Schemas, Slowly Changing Dimensions (SCD Type 1, 2, 3), surrogate keys.
- **Curriculum Integration**: [[MOD-02 - Kimball Dimensional Modeling]] through [[MOD-05 - Slowly Changing Dimensions]].

### 3. Fundamentals of Data Engineering
- **Authors**: Joe Reis & Matt Housley
- **Publisher**: O'Reilly Media
- **Official URL**: [oreilly.com/library/view/fundamentals-of-data/9781098108298/](https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/)
- **Core Topics**: The Data Engineering lifecycle, generation, storage, ingestion, transformation, serving, security, data ops.
- **Curriculum Integration**: [[DBT-01 - Modern ELT Architecture]], [[LAK-01 - Object Storage Architecture]], [[DES-01 - System Design Interview Framework]].

### 4. Fluent Python (2nd Edition)
- **Author**: Luciano Ramalho
- **Publisher**: O'Reilly Media
- **Official URL**: [oreilly.com/library/view/fluent-python-2nd/9781492056348/](https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/)
- **Core Topics**: Iterators, generators, context managers, decorators, type hints, protocols, memory efficiency.
- **Curriculum Integration**: [[PY-04 - Functional Mechanics and Itertools]] through [[PY-08 - Context Managers]].

### 5. Pro Git (2nd Edition)
- **Authors**: Scott Chacon & Ben Straub
- **Publisher**: Apress (100% Free Official eBook)
- **Official URL**: [git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
- **Core Topics**: Git object model (blobs, trees, commits), branching mechanics, interactive rebasing, merge strategies.
- **Curriculum Integration**: [[GIT-01 - Git Internals and Staging]] through [[GIT-04 - Semantic Versioning]].

### 6. Apache Iceberg: The Definitive Guide
- **Authors**: Tomer Shiran, Jason Hughes, Alex Merced
- **Publisher**: O'Reilly / Dremio (Free Official Community eBook)
- **Official URL**: [dremio.com/resources/guides/apache-iceberg-the-definitive-guide/](https://www.dremio.com/resources/guides/apache-iceberg-the-definitive-guide/)
- **Core Topics**: Open table format mechanics, snapshot isolation, hidden partitioning, metadata trees, schema evolution.
- **Curriculum Integration**: [[LAK-04 - Open Table Format Paradigm]] through [[LAK-06 - Iceberg Hidden Partitioning]].

### 7. Kafka: The Definitive Guide (2nd Edition)
- **Authors**: Gwen Shapira, Todd Palino, Rajini Sivaram, Krit Petty
- **Publisher**: O'Reilly / Confluent (Free Official Community eBook)
- **Official URL**: [confluent.io/resources/kafka-the-definitive-guide-2nd-edition/](https://www.confluent.io/resources/kafka-the-definitive-guide-2nd-edition/)
- **Core Topics**: Event streaming architecture, KRaft consensus, partition leaders, consumer groups, exactly-once semantics.
- **Curriculum Integration**: [[KFK-01 - Event-Driven Fundamentals]] through [[KFK-06 - Delivery Guarantees]].

### 8. Learning Spark (2nd Edition)
- **Authors**: Jules S. Damji, Brooke Wenig, Tathagata Das, Denny Lee
- **Publisher**: O'Reilly Media
- **Official URL**: [oreilly.com/library/view/learning-spark-2nd/9781492050032/](https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/)
- **Core Topics**: Apache Spark architecture, DataFrame API, Catalyst optimizer, Spark SQL, shuffle operations.
- **Curriculum Integration**: [[SPK-01 - Spark 4 Cluster Architecture]] through [[SPK-07 - Join Strategies in Spark]].
