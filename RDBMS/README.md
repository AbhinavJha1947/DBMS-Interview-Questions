# RDBMS Fundamentals & Database Concepts

Welcome to the RDBMS Interview Questions repository. This guide covers everything from core database concepts to advanced design patterns, organized in a Question & Answer format.

## Table of Contents

1. [Core Database Concepts](#1-core-database-concepts)
2. [Data Types](#2-data-types)
3. [Schema, Catalog & Nullability](#3-schema-catalog--nullability)
4. [Keys & Constraints](#4-keys--constraints)
5. [Normalization & Denormalization](#5-normalization--denormalization)
6. [ACID, BASE, and CAP](#6-acid-base-and-cap)
7. [Indexing](#7-indexing)
8. [Transaction Management & Concurrency](#8-transaction-management--concurrency)
9. [Database Design Patterns](#9-database-design-patterns)

---

## 1. Core Database Concepts

### What is a database?
- A persistent, organized collection of structured data plus metadata enabling efficient storage, retrieval, security, integrity, and performance.
- **Core components**: data files, catalog (schema metadata), transaction log/WAL, buffer pool, query optimizer, execution engine, lock/MVCC manager, background maintenance (VACUUM, checkpoints, statistics).

### What is the difference between DBMS and RDBMS?
- **DBMS**: generic data management; may be hierarchical, network, document, key–value, etc.
- **RDBMS**: implements the relational model with relations (tables), tuples (rows), attributes (columns), schemas, keys, SQL, ACID, normalization, and declarative constraints.
- **Practical upshot**: portability of concepts, stricter integrity, transaction guarantees.

### What is the Relational Model?
- Relation = table; tuple = row; attribute = column; schema = relation definition.
- **Properties**: set semantics, logical independence, closure (results are relations), declarative algebra (projection, selection, join, union, difference).
- **Benefits**: predictable constraints and optimizations; decouples logical design from physical storage.

### What are tables, rows, and columns?
- Tables model entities or relationships; rows are instances; columns are typed attributes with constraints (NOT NULL, CHECK, DEFAULT, UNIQUE, FK).
- Keys enforce uniqueness; foreign keys enforce relationships; NULL indicates unknown/not applicable.

### What is ER modeling?
- Capture entities, attributes, relationships; specify cardinality and optionality; identify keys.
- **Mapping**: entities → tables; attributes → columns; identifiers → primary keys; relationships → foreign keys or junction tables.

### What are the different relationship types (1:1, 1:N, M:N)?
- **1:1**: unique FK or merge tables (when lifecycles coincide).
- **1:N**: FK on N-side referencing 1-side PK; consider ON DELETE/UPDATE actions (CASCADE, SET NULL, RESTRICT/NO ACTION).
- **M:N**: junction/bridge table with two FKs; composite PK or surrogate key plus UNIQUE pair.

### What is the difference between Logical and Physical Schema design?
- **Logical**: tables, columns, data types, constraints, views, normalization, naming, governance.
- **Physical**: indexing strategy, partitioning (range, list, hash), fill factor, compression/columnstore, filegroups/tablespaces, autovacuum/VACUUM, stats.
- **Flow**: model → normalize → validate workloads → add indexes/partitions/materializations → iterate.

[Back to Top](#table-of-contents)

---

## 2. Data Types

### What are the guiding principles for choosing Data Types?
- Choose the narrowest type; match units and precision; avoid over-wide VARCHAR; prefer DATE/TIMESTAMP over strings.

### What are the common Numeric data types?
- **INT/SMALLINT/BIGINT**: whole numbers; choose the smallest that fits to reduce I/O and index size.
- **DECIMAL/NUMERIC(p,s)**: exact fixed-point; use for money and precise totals; beware `s` for scale.
- **FLOAT/REAL/DOUBLE**: approximate; avoid for money; good for scientific measurements.
- **Pitfalls**: implicit casts hurt SARGability; mismatched types between JOIN/WHERE hinder index use.

### What are String data types and what is Collation?
- **CHAR(n)**: fixed-width; pad with spaces; use for stable-length codes only.
- **VARCHAR(n)**: variable; prefer over CHAR for most text; size `n` gates validation.
- **TEXT/CLOB**: long text; limited indexing; use full-text indexes for search.
- **Collation**: sort/compare rules; case and accent sensitivity affect DISTINCT, ORDER BY, JOINs.

### How are Date and Time handled in RDBMS?
- DATE, TIME, TIMESTAMP/DATETIME; WITH TIME ZONE variants are vendor-specific; INTERVAL types in some vendors.
- **Guidelines**: store UTC; convert at edges; use proper types for durations; avoid string dates.
- **Gotchas**: DST transitions; implicit conversions; precision differences (e.g., datetime vs datetime2).

### What are Boolean / BIT types?
- TRUE/FALSE (PostgreSQL), 0/1 (MySQL TINYINT), BIT (SQL Server). Normalize semantics in app.

### What are Binary data types?
- BINARY/VARBINARY, BYTEA; good for hashes/small binaries; large objects often better in object storage.

### How is Semi‑structured data (JSON/XML) handled?
- JSON/JSONB (PostgreSQL), JSON (MySQL), SQL Server JSON functions; XML types.
- **Indexing**: GIN (jsonb) in PG; generated columns + B‑tree in MySQL; PATH/secondary indexes in others.
- **Validation**: CHECK constraints, JSON schema features (PG extensions), or app-level checks.

### What is the quick guide for choosing Data Types?
- **IDs**: BIGINT identity/serial or UUID (prefer v7 over v4 for index locality where available).
- **Money**: DECIMAL(19,4) exact types, not FLOAT.
- **Text search**: TEXT + full‑text index; avoid leading‑wildcard LIKE.
- **Analytics**: columnstore + compressed types for scans.

[Back to Top](#table-of-contents)

---

## 3. Schema, Catalog & Nullability

### What are Schema and Catalog?
- **Schema**: namespace for objects; simplifies permissions and organization.
- **Catalog/Database**: groups schemas; qualify names as catalog.schema.object per vendor.
- **Cross‑database references**: vary (e.g., SQL Server three‑part names; PostgreSQL favors schemas within one database).

### What is Nullability and Three-valued Logic?
- NULL propagates to UNKNOWN in predicates; WHERE filters UNKNOWN; watch NULLs in outer joins and aggregates.
- **Tools**: IS NULL/IS NOT NULL, COALESCE/ISNULL/IFNULL, NULLIF, SET DEFAULT, CHECK/NOT NULL.
- **Tip**: Prefer NOT NULL with sensible DEFAULTs to simplify logic and improve index selectivity.

### What is the difference between OLTP and OLAP?
- **OLTP**: high concurrency, short transactions, low latency; normalized 3NF/BCNF; B‑tree indexes; rowstore engines.
- **OLAP**: scans, aggregates, star/snowflake; columnstore indexes; partitioning; batch ETL/ELT; materialized views.
- **Bridging**: CDC to warehouse, HTAP systems, summary tables.

[Back to Top](#table-of-contents)

---

## 4. Keys & Constraints

### What is a Primary Key?
- **Definition**: Column or set of columns that uniquely identifies each row. Must be UNIQUE and NOT NULL. One per table.
- **Surrogate vs Natural**: Surrogate (IDENTITY/SEQUENCE/UUID) is stable and narrow; Natural uses domain attributes but can change.
- **Entity Integrity**: ensure every row is identifiable.

### What is a Foreign Key?
- **Definition**: Column(s) referencing a parent table’s PK or UNIQUE key to enforce referential integrity.
- **Actions**: NO ACTION/RESTRICT, CASCADE, SET NULL, SET DEFAULT.
- **Referential Integrity**: ensure relationships are consistent across tables.

### What is a Unique Key?
- **Definition**: Enforces uniqueness of values across rows. Unlike PK, it may allow NULLs depending on the vendor.
- **Use Case**: Use UNIQUE(email) for natural identifiers even when using surrogate PK.

### What is the difference between Natural Key and Surrogate Key?
- **Natural**: Derived from business data. Pro: inherent meaning. Con: can change, wider.
- **Surrogate**: Artificial (ID). Pro: stable, narrow. Con: needs additional UNIQUE for business rules.

### What are Candidate, Alternate, and Super Keys?
- **Candidate Key**: Minimal column set that can uniquely identify rows.
- **Alternate Key**: Candidate key not chosen as PK.
- **Super Key**: Any superset of a candidate key.

### What are Composite Keys?
- **Definition**: Multi-column keys (PK or UNIQUE).
- **Ordering**: Leftmost prefix rule applies for index performance.

### What are Check Constraints?
- **Definition**: Boolean expressions that must be TRUE for each row.
- **Example**: `CHECK (age BETWEEN 0 AND 120)`. Part of **Domain Integrity**.

### What are Default and NOT NULL constraints?
- **DEFAULT**: Provides a value when none is supplied on INSERT.
- **NOT NULL**: Disallows NULL values. Prefer combining with sensible defaults.

### What are enforcement tips for constraints?
- Prefer constraints over triggers for validation; they are declarative and optimized.

[Back to Top](#table-of-contents)

---

## 5. Normalization & Denormalization

### What is the purpose and benefit of Normalization?
- **Goal**: Reduce redundancy, prevent anomalies (Insertion, Update, Deletion), and ensure each fact is stored once.

### What are Functional Dependencies (FDs)?
- **Definition**: X → Y means X functionally determines Y. Used to derive keys and decide on decompositions.

### Explain the various Normal Forms (1NF to 5NF).
- **1NF**: Atomic values only, no repeating groups.
- **2NF**: No partial dependencies (on composite keys).
- **3NF**: No transitive dependencies. "Depends on key, whole key, nothing but the key."
- **BCNF**: Stricter version of 3NF where every determinant is a super key.
- **4NF**: Handles multi-valued dependencies.
- **5NF**: Handles join dependencies.

### What are Database Anomalies?
- **Insertion**: Cannot add data without unrelated facts.
- **Update**: Risk of inconsistency when updating redundant data.
- **Deletion**: Unintentional loss of data when deleting a related fact.

### What is Denormalization and when should it be used?
- **Purpose**: Speed up reads, reduce joins, enable precomputed aggregates.
- **Trade-off**: Write amplification, storage overhead, and consistency complexity.

### What is a quick workflow for Normalization?
1. List attributes and candidate keys.
2. Elicit FDs and find minimal cover.
3. Ensure 1NF -> 2NF -> 3NF.
4. Add constraints and indexes.
5. Consider targeted denormalization for hotspots.

[Back to Top](#table-of-contents)

---

## 6. ACID, BASE, and CAP

### What are ACID properties?
- **Atomicity**: All or nothing.
- **Consistency**: Moves DB from one valid state to another.
- **Isolation**: Concurrent transactions don't interfere.
- **Durability**: Committed changes survive crashes (WAL).

### What are the different Transaction Isolation Levels?
- **Read Uncommitted**: Allows dirty reads.
- **Read Committed**: Prevents dirty reads (Default for many).
- **Repeatable Read**: Prevents non-repeatable reads.
- **Serializable**: Highest isolation, prevents phantoms.
- **Snapshot Isolation**: MVCC-based consistency without blocking readers.

### What are the common Isolation Phenomena (Anomalies)?
- **Dirty Read**: Reading uncommitted data.
- **Non-repeatable Read**: Value changes between two reads in the same transaction.
- **Phantom Read**: Set of rows changes between reads.
- **Lost Update**: Two writers overwrite each other.
- **Write Skew**: Snapshot isolation anomaly where two transactions overlap inconsistently.

### What is BASE and Eventual Consistency?
- **Basically Available**, **Soft State**, **Eventual Consistency**.
- Used in distributed systems for high availability and low latency at the cost of immediate consistency.

### What is the CAP Theorem?
- In the presence of a **Network Partition (P)**, you must choose between **Consistency (C)** and **Availability (A)**.

[Back to Top](#table-of-contents)

---

## 7. Indexing

### How do Indexes work?
- Speed up lookups and joins by maintaining ordered structures (B-Trees) over key columns.
- **Selectivity**: High selectivity (unique values) makes indexes efficient.

### What are common Index Structures (B-Tree, B+Tree)?
- **B-Tree**: Balanced trees.
- **B+Tree**: Data only in leaves, linked for efficient range scans.

### What are Clustered and Non-Clustered Indexes?
- **Clustered**: Tables stored in index order (one per table).
- **Non-Clustered**: Pointers to rows or clustered keys (many per table).
- **Covering Index**: Answers query entirely from index (`INCLUDE` columns).

### What are key Performance Concepts in Indexing?
- **Index Seek**: Targeted lookup.
- **Index Scan**: Full walk of the index.
- **SARGability**: Predicates that can use indexes (avoid functions on columns).
- **Fragmentation**: Requires rebuild/reorganize maintenance.

[Back to Top](#table-of-contents)

---

## 8. Transaction Management & Concurrency

### What is the Transaction Lifecycle?
- **BEGIN** -> **Operations** -> **COMMIT** or **ROLLBACK**.
- **SAVEPOINT**: Partial rollbacks within a transaction.

### What is MVCC?
- **Multi-Version Concurrency Control**. Writers don't block readers; readers don't block writers. Uses versions (xid/undo) to maintain consistency.

### What are the different Locking modes and granularities?
- **Modes**: Shared (S), Exclusive (X), Update (U), Intent Locks.
- **Granularity**: Row, Page, Table.
- **Deadlock**: Cycle of dependencies. Prevent by consistent access order and indexing.

### What is the difference between Optimistic and Pessimistic Concurrency?
- **Pessimistic**: Prevents conflicts with locks. Best for high write contention.
- **Optimistic**: Detects conflicts at commit (versions). Best for read-heavy workloads.

[Back to Top](#table-of-contents)

---

## 9. Database Design Patterns

### Explain Star and Snowflake Schemas.
- **Star**: Central Fact table with denormalized Dimension tables.
- **Snowflake**: Normalized dimensions (reduces redundancy, adds joins).

### What are the different types of Fact Tables?
- **Transaction Fact**: One row per event.
- **Periodic Snapshot**: Summaries at intervals.
- **Accumulating Snapshot**: Tracks lifecycle stages.

### What are Junk, Degenerate, and Bridge Dimensions?
- **Junk**: Grouping low-cardinality flags.
- **Degenerate**: ID stored in fact table (no dim table).
- **Bridge**: Resolves Many-to-Many relationships.

### What are Slowly Changing Dimensions (SCD Types 1, 2, 3)?
- **Type 1**: Overwrite history.
- **Type 2**: Add new row (full history).
- **Type 3**: Add "previous value" column (limited history).

### What is the difference between Operational and Analytical databases?
- **OLTP**: Normalized (3NF), current state, low latency.
- **OLAP**: Denormalized (Star/Snowflake), historical snapshots, massive aggregates.

[Back to Top](#table-of-contents)
