# RDBMS Fundamentals & Database Concepts

Welcome to the RDBMS Interview Questions repository. This guide consists of 50+ granular topics covering everything from core architecture to advanced analytical design patterns.

## Table of Contents

### 1. Database Basics & Architecture
- 1.1 [What is a Database?](#11-what-is-a-database)
- 1.2 [What is the difference between DBMS and RDBMS?](#12-what-is-the-difference-between-dbms-and-rdbms)
- 1.3 [What is the Relational Model and its properties?](#13-what-is-the-relational-model-and-its-properties)
- 1.4 [What are the benefits of the Relational Model?](#14-what-are-the-benefits-of-the-relational-model)
- 1.5 [What are Tables, Rows, and Columns?](#15-what-are-tables-rows-and-columns)
- 1.6 [What is ER (Entity-Relationship) Modeling?](#16-what-is-er-entity-relationship-modeling)
- 1.7 [What are the types of Relationships (1:1, 1:N, M:N)?](#17-what-are-the-types-of-relationships-11-1n-mn)
- 1.8 [What is the difference between Logical and Physical Schema?](#18-what-is-the-difference-between-logical-and-physical-schema)

### 2. Data Types & Storage
- 2.1 [What are the principles for choosing Data Types?](#21-what-are-the-principles-for-choosing-data-types)
- 2.2 [Numeric Data Types: INT, DECIMAL, vs FLOAT](#22-numeric-data-types-int-decimal-vs-float)
- 2.3 [String Data Types & Collation (CHAR vs VARCHAR)](#23-string-data-types--collation-char-vs-varchar)
- 2.4 [Handling Date, Time, and Timezones](#24-handling-date-time-and-timezones)
- 2.5 [Working with Semi-structured Data (JSON/XML)](#25-working-with-semi-structured-data-jsonxml)
- 2.6 [Choosing Primary Key Types: BIGINT vs UUID](#26-choosing-primary-key-types-bigint-vs-uuid)
- 2.7 [Three-Valued Logic and NULL Handling](#27-three-valued-logic-and-null-handling)
- 2.8 [Binary Data Types: BLOB and BYTEA](#28-binary-data-types-blob-and-bytea)

### 3. Constraints & Integrity
- 3.1 [What is Entity Integrity (Primary Keys)?](#31-what-is-entity-integrity-primary-keys)
- 3.2 [What is Referential Integrity (Foreign Keys)?](#32-what-is-referential-integrity-foreign-keys)
- 3.3 [Foreign Key Actions: CASCADE, SET NULL, RESTRICT](#33-foreign-key-actions-cascade-set-null-restrict)
- 3.4 [What is Domain Integrity? (CHECK, DEFAULT, NOT NULL)](#34-what-is-domain-integrity-check-default-not-null)
- 3.5 [Unique Constraints and Business Identifiers](#35-unique-constraints-and-business-identifiers)
- 3.6 [Assertion and Triggers vs Constraints](#36-assertion-and-triggers-vs-constraints)

### 4. Normalization Deep Dive
- 4.1 [What is the purpose of Normalization?](#41-what-is-the-purpose-of-normalization)
- 4.2 [What are Functional Dependencies (FDs)?](#42-what-are-functional-dependencies-fds)
- 4.3 [1NF: Atomic Values and Repeating Groups](#43-1nf-atomic-values-and-repeating-groups)
- 4.4 [2NF: Removing Partial Dependencies](#44-2nf-removing-partial-dependencies)
- 4.5 [3NF: Removing Transitive Dependencies](#45-3nf-removing-transitive-dependencies)
- 4.6 [BCNF: Boyce–Codd Normal Form](#46-bcnf-boycecodd-normal-form)
- 4.7 [4NF: Multi-valued Dependencies (MVDs)](#47-4nf-multi-valued-dependencies-mvds)
- 4.8 [5NF: Join Dependencies (PJ/NF)](#48-5nf-join-dependencies-pjnf)
- 4.9 [What are Database Anomalies?](#49-what-are-database-anomalies)
- 4.10 [Denormalization: When and Why?](#410-denormalization-when-and-why)
- 4.11 [Standard Normalization Workflow](#411-standard-normalization-workflow)

### 5. Transactions & Concurrency
- 5.1 [ACID Properties Deep Dive](#51-acid-properties-deep-dive)
- 5.2 [Atomicity: Rollback and WAL](#52-atomicity-rollback-and-wal)
- 5.3 [Consistency: Database State Invariants](#53-consistency-database-state-invariants)
- 5.4 [Isolation Levels and ANSI Standards](#54-isolation-levels-and-ansi-standards)
- 5.5 [Isolation Phenomena: Dirty Read, Phantoms, Write Skew](#55-isolation-phenomena-dirty-read-phantoms-write-skew)
- 5.6 [Durability: Disk Flushing and Checkpoints](#56-durability-disk-flushing-and-checkpoints)
- 5.7 [What is MVCC (Multi-Version Concurrency Control)?](#57-what-is-mvcc-multi-version-concurrency-control)
- 5.8 [Locking Mechanisms: S, X, U, and Intent Locks](#58-locking-mechanisms-s-x-u-and-intent-locks)
- 5.9 [Deadlocks: Detection and Resolution](#59-deadlocks-detection-and-resolution)
- 5.10 [Optimistic vs Pessimistic Concurrency](#510-optimistic-vs-pessimistic-concurrency)
- 5.11 [What is the CAP Theorem?](#511-what-is-the-cap-theorem)
- 5.12 [Why is Partition Tolerance mandatory in Distributed Systems?](#512-why-is-partition-tolerance-mandatory-in-distributed-systems)
- 5.13 [Detailed Comparison: CP vs AP Systems](#513-detailed-comparison-cp-vs-ap-systems)
- 5.14 [What is the BASE Model?](#514-what-is-the-base-model)
- 5.15 [Strong Consistency vs Eventual Consistency](#515-strong-consistency-vs-eventual-consistency)
- 5.16 [What is the PACELC Theorem?](#516-what-is-the-pacelc-theorem)

### 6. Indexing & Performance
- 6.1 [How do Indexes work?](#61-how-do-indexes-work)
- 6.2 [B-Tree vs B+Tree Index Structures](#62-b-tree-vs-bplus-tree-index-structures)
- 6.3 [Clustered vs Non-Clustered Indexes](#63-clustered-vs-non-clustered-indexes)
- 6.4 [Composite Indexes: The Leftmost Prefix Rule](#64-composite-indexes-the-leftmost-prefix-rule)
- 6.5 [What is a Covering Index?](#65-what-is-a-covering-index)
- 6.6 [SARGability: Writing Index-Optimized Queries](#66-sargability-writing-index-optimized-queries)
- 6.7 [Full-Text Search and Specialized Indexes (GIN/GiST)](#67-full-text-search-and-specialized-indexes-gingist)
- 6.8 [Index Fragmentation and Maintenance](#68-index-fragmentation-and-maintenance)

### 7. Database Design Patterns (OLAP)
- 7.1 [OLTP vs OLAP Architecture](#71-oltp-vs-olap-architecture)
- 7.2 [Star Schema: Facts and Dimensions](#72-star-schema-facts-and-dimensions)
- 7.3 [Snowflake Schema: Normalized Dimensions](#73-snowflake-schema-normalized-dimensions)
- 7.4 [Fact Tables: Transactional vs Snapshot](#74-fact-tables-transactional-vs-snapshot)
- 7.5 [Dimension Types: Junk, Degenerate, Bridge](#75-dimension-types-junk-degenerate-bridge)
- 7.6 [SCD Types 1, 2, and 3 (Slowly Changing Dimensions)](#76-scd-types-1-2-and-3-slowly-changing-dimensions)

---

## 1. Database Basics & Architecture

### 1.1 What is a Database?
- A persistent, organized collection of structured data plus metadata enabling efficient storage, retrieval, security, integrity, and performance.
- **Core components**: data files, catalog (schema metadata), transaction log/WAL, buffer pool, query optimizer, execution engine, lock/MVCC manager, background maintenance (VACUUM, checkpoints, statistics).

### 1.2 What is the difference between DBMS and RDBMS?
- **DBMS**: generic data management; may be hierarchical, network, document, key–value, etc.
- **RDBMS**: implements the relational model with relations (tables), tuples (rows), attributes (columns), schemas, keys, SQL, ACID, normalization, and declarative constraints.
- **Practical upshot**: portability of concepts, stricter integrity, transaction guarantees.

### 1.3 What is the Relational Model and its properties?
- **Definition**: A data model based on first-order predicate logic where data is represented as relations (tables).
- **Properties**: 
    - **Set Semantics**: Rows are unordered and unique.
    - **Logical Independence**: The application is decoupled from the physical storage.
    - **Closure**: The result of a relational operation is itself a relation.
    - **Declarative Algebra**: Operations like Projection, Selection, Join, Union.

### 1.4 What are the benefits of the Relational Model?
- **Predictability**: Strict schemas ensure data consistency.
- **Optimization**: The query optimizer can determine the best execution path without programmer intervention.
- **Decoupling**: Changes to physical storage (indexes, partitions) don't require rewriting application code.

### 1.5 What are Tables, Rows, and Columns?
- **Tables**: Model entities (e.g., Users) or relationships (e.g., Orders).
- **Rows (Tuples)**: Specific instances of an entity.
- **Columns (Attributes)**: Typed properties of the entity (e.g., Email, BirthDate) with constraints like `NOT NULL`.

### 1.6 What is ER (Entity-Relationship) Modeling?
- A high-level conceptual data model used to capture the requirements of a database.
- **Goal**: Identify Entities (nouns), Attributes (adjectives), and Relationships (verbs).
- **Mapping**: Entities become tables, attributes become columns, and identifiers become primary keys.

### 1.7 What are the types of Relationships (1:1, 1:N, M:N)?
- **1:1**: One row in Table A relates to exactly one in Table B. Often merged or linked via unique Foreign Key.
- **1:N**: One row in Table A relates to many in Table B. Requires a Foreign Key on the "N" side.
- **M:N**: Many rows in Table A relate to many in Table B. Requires a **Junction/Bridge Table** with two Foreign Keys.

### 1.8 What is the difference between Logical and Physical Schema?
- **Logical Schema**: Focuses on data organization (tables, columns, normalization, naming conventions).
- **Physical Schema**: Focuses on performance and storage (indexing, partitioning, compression, filegroups, tablespaces).

[Back to Top](#table-of-contents)

---

## 2. Data Types & Storage

### 2.1 What are the principles for choosing Data Types?
- **Narrowest Type**: Choose the smallest size that fits the data to reduce I/O.
- **Consistency**: Match units (e.g., USD, grams) and precision across the system.
- **Native Types**: Prefer native types (DATE/TIMESTAMP) over strings to enable indexing and date math.

### 2.2 Numeric Data Types: INT, DECIMAL, vs FLOAT
- **INT/BIGINT**: For whole numbers and primary keys.
- **DECIMAL(p,s)**: Exact fixed-point for money and precise calculations.
- **FLOAT/DOUBLE**: Approximate precision for scientific measurements; **never use for money**.

### 2.3 String Data Types & Collation (CHAR vs VARCHAR)
- **CHAR(n)**: Fixed-width; pads with spaces. Use for stable-length codes (e.g., ISO Country Codes).
- **VARCHAR(n)**: Variable-width. Use for most text. `n` restricts the max length.
- **Collation**: Rules for sorting and comparing characters (e.g., Case Sensitivity, Accent Sensitivity).

### 2.4 Handling Date, Time, and Timezones
- **DATE**: YYYY-MM-DD.
- **TIMESTAMP/DATETIME**: Includes time component.
- **Best Practice**: Always store dates in **UTC** at the database level and convert to the user's timezone at the application/UI level.

### 2.5 Working with Semi-structured Data (JSON/XML)
- Modern RDBMS (PostgreSQL, SQL Server, MySQL) support JSON types.
- **JSONB** (PostgreSQL): Binary format that is indexable via GIN indexes.
- **Use Case**: Great for flexible schemas or sparse attributes, but avoid for core relational data to maintain 1NF.

### 2.6 Choosing Primary Key Types: BIGINT vs UUID
- **BIGINT**: High performance, ever-increasing (good for B-Tree locality), but exposes record counts.
- **UUID (v7)**: Globally unique, non-sequential (though v7 is time-ordered), hides record counts, but wider (16 bytes vs 8).

### 2.7 Three-Valued Logic and NULL Handling
- SQL uses **TRUE, FALSE, and UNKNOWN**.
- `NULL = NULL` is UNKNOWN, not TRUE.
- **Tip**: Prefer `NOT NULL` with sensible defaults (e.g., `0`) to simplify application logic and improve index selectivity.

### 2.8 Binary Data Types: BLOB and BYTEA
- Used for storing small binaries (hashes, salt) or smaller images.
- **Tip**: For large files (MP4s, high-res images), store them in Object Storage (S3/Azure Blob) and store only the URL/Path in the database.

[Back to Top](#table-of-contents)

---

## 3. Constraints & Integrity

### 3.1 What is Entity Integrity (Primary Keys)?
- Ensures that every row in a table is uniquely identifiable and that the primary key is never NULL.
- **Surrogate PK**: Artificial ID (Serial/Auto-increment).
- **Natural PK**: Real-world unique identifier (e.g., SSN, Email) - risky if business rules change.

### 3.2 What is Referential Integrity (Foreign Keys)?
- Ensures that the relationship between two tables remains consistent. A Foreign Key in a child table must exist as a Primary Key in the parent table.

### 3.3 Foreign Key Actions: CASCADE, SET NULL, RESTRICT
- **CASCADE**: Deleting/Updating parent also deletes/updates children.
- **SET NULL**: Parent deletion sets child FK to NULL.
- **RESTRICT/NO ACTION**: Prevents deletion of the parent if children exist.

### 3.4 What is Domain Integrity? (CHECK, DEFAULT, NOT NULL)
- **CHECK**: Enforces custom rules (e.g., `CHECK (price > 0)`).
- **DEFAULT**: Provides a value if none is supplied.
- **NOT NULL**: Prevents missing data.

### 3.5 Unique Constraints and Business Identifiers
- Enforces that all values in a column are unique.
- Useful for columns that aren't the Primary Key but must be distinct, like Usernames or Passport Numbers.

### 3.6 Assertion and Triggers vs Constraints
- **Constraints**: Declarative, fast, and optimized by the engine.
- **Triggers**: Procedural, slower, and harder to debug. Use constraints whenever possible.

[Back to Top](#table-of-contents)

---

## 4. Normalization Deep Dive

### 4.1 What is the purpose of Normalization?
- Goal: **Reduce redundancy**, prevent integrity anomalies, and ensure each "fact" is stored exactly once.

### 4.2 What are Functional Dependencies (FDs)?
- If column A determines column B (`A -> B`), then for every value of A, there is one and only one value of B. This is the foundation of normalization.

### 4.3 1NF: Atomic Values and Repeating Groups
- No multi-valued attributes (arrays, comma-separated lists).
- Each column must contain atomic (indivisible) values.

### 4.4 2NF: Removing Partial Dependencies
- Applies to composite primary keys. No non-key attribute should depend on only a *part* of a composite key.

### 4.5 3NF: Removing Transitive Dependencies
- No non-key attribute should depend on another non-key attribute. "Attributes must depend on the key, the whole key, and nothing but the key."

### 4.6 BCNF: Boyce–Codd Normal Form
- A stricter version of 3NF. For every functional dependency `X -> Y`, `X` must be a super key.

### 4.7 4NF: Multi-valued Dependencies (MVDs)
- Removes independent multi-valued facts. For example, if a "Chef" has multiple "Specialties" AND multiple "Languages", these should be in separate tables.

### 4.8 5NF: Join Dependencies (PJ/NF)
- A table is in 5NF if it cannot be decomposed into smaller tables that, when joined back, produce spurious rows.

### 4.9 What are Database Anomalies?
- **Insertion**: Can't add a student unless they join a course.
- **Update**: Changing a course name requires updating 1000 student rows.
- **Deletion**: Deleting the last student in a course accidentally deletes the course info.

### 4.10 Denormalization: When and Why?
- Used to speed up reads in reporting/OLAP environments by reducing the number of joins.
- **Costs**: Slower writes, increased storage, and risk of data inconsistency.

### 4.11 Standard Normalization Workflow
1. Identify all functional dependencies.
2. Break into 1NF (atomicity).
3. Break into 2NF (remove partial dependencies).
4. Break into 3NF (remove transitive dependencies).
5. Refine into BCNF/4NF if complex relationships exist.

[Back to Top](#table-of-contents)

---

## 5. Transactions & Concurrency

### 5.1 ACID Properties Deep Dive
- **Atomicity**: All or nothing.
- **Consistency**: Database moves from one valid state to another.
- **Isolation**: Concurrent transactions don't interfere.
- **Durability**: Committed data is permanent.

### 5.2 Atomicity: Rollback and WAL
- Guaranteed via **Write-Ahead Logging (WAL)**. Changes are written to the log first; if a crash occurs, the DB uses the log to redo or undo changes.

### 5.3 Consistency: Database State Invariants
- Enforced through constraints (PK, FK, CHECK). If a transaction violates a constraint, the whole transaction is rolled back to maintain consistency.

### 5.4 Isolation Levels and ANSI Standards
- **Read Uncommitted**: See uncommitted data (Dirty Read).
- **Read Committed**: Only see committed data (Default).
- **Repeatable Read**: Re-reading a row gives the same result.
- **Serializable**: Full sequential execution behavior.

### 5.5 Isolation Phenomena: Dirty Read, Phantoms, Write Skew
- **Dirty Read**: Reading uncommitted data.
- **Non-Repeatable Read**: Row value changes between two reads.
- **Phantom Read**: New rows appear in a range query.
- **Write Skew**: A concurrency anomaly where two transactions overlap and result in a logically invalid state (common in Snapshot Isolation).

### 5.6 Durability: Disk Flushing and Checkpoints
- Commits are only acknowledged once the log is flushed to physical disk. **Checkpoints** periodically sync the data files with the log to speed up recovery.

### 5.7 What is MVCC (Multi-Version Concurrency Control)?
- A method to allow readers and writers to operate without blocking each other. Each reader sees a "snapshot" (version) of the data from the time the transaction started.

### 5.8 Locking Mechanisms: S, X, U, and Intent Locks
- **Shared (S)**: For reading.
- **Exclusive (X)**: For writing.
- **Update (U)**: Prevents deadlocks during read-then-write operations.
- **Intent Locks**: Signal that a lower-level (row) lock is held.

### 5.9 Deadlocks: Detection and Resolution
- A cycle where Transaction A waits for B, and B waits for A.
- **Resolution**: The DB engine detects the cycle and "kills" one transaction (the victim) to let the other proceed.

### 5.10 Optimistic vs Pessimistic Concurrency
- **Pessimistic**: Locks data immediately. Good for high write contention.
- **Optimistic**: No initial locks; checks for changes at commit time (using a version/timestamp). Good for read-heavy apps.

### 5.11 What is the CAP Theorem?
- **Consistency**: Every read receives the most recent write or an error.
- **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
- **Partition Tolerance**: The system continues to operate despite an arbitrary number of messages being dropped or delayed by the network between nodes.
- **The Trade-off**: In a distributed system, partitions (P) are inevitable (network failures). Therefore, when a partition occurs, you must choose between C (Stop serving requests to stay consistent) or A (Serve potentially stale data to stay available).

### 5.12 Why is Partition Tolerance mandatory in Distributed Systems?
- Networks are unreliable. You cannot guarantee perfect communication between nodes.
- Since P is a given, the real choice is between **CP** (Consistency over Availability) and **AP** (Availability over Consistency).

### 5.13 Detailed Comparison: CP vs AP Systems
- **CP (Consistency / Partition Tolerance)**:
    - **Behavior**: When a partition occurs, the system protects consistency. It may reject writes or reads if it cannot guarantee the data is up-to-date.
    - **Examples**: HBase, MongoDB (default), Redis (Sentinel/Cluster), RDBMS with synchronous replication.
    - **Use Case**: Financial systems, Inventory management (double-booking is unacceptable).
- **AP (Availability / Partition Tolerance)**:
    - **Behavior**: Prioritizes uptime. Nodes accept writes even if they cannot communicate with peers. Data reconciles later.
    - **Examples**: Cassandra, DynamoDB, Couchbase, DNS.
    - **Use Case**: Social media feeds, Shopping carts, Real-time analytics where staleness is tolerable.

### 5.14 What is the BASE Model?
- **Basically Available**: The system guarantees availability (often using replication).
- **Soft State**: The state of the system may change over time, even without input (due to background syncing).
- **Eventual Consistency**: The system will stop changing and become consistent once it stops receiving input.
- **Contrast**: BASE is the philosophy for AP systems, while ACID is for CP/Single-node systems.

### 5.15 Strong Consistency vs Eventual Consistency
- **Strong Consistency**: Linearity. After a write is acknowledged, any subsequent read (from any node) returns that value.
- **Eventual Consistency**: After a write, reads may return stale values for a short period (inconsistency window), but all nodes will eventually converge.
- **Read-Your-Writes**: A consistency model where a user always sees their own updates, even if other users see stale data.

### 5.16 What is the PACELC Theorem?
- An extension to CAP describing trade-offs during *normal* operations.
- **Statement**: If there is a Partition (P), choose between Availability (A) and Consistency (C). **Else (E)** (no partition), choose between Latency (L) and Consistency (C).
- **Significance**: CAP only explains failure modes. PACELC explains why synchronous replication (Consistency) slows down the system (Latency) even when the network is fine.

[Back to Top](#table-of-contents)

---

## 6. Indexing & Performance

### 6.1 How do Indexes work?
- Indexes are secondary data structures (usually B-Trees) that allow the engine to find rows without scanning the entire table.

### 6.2 B-Tree vs B+Tree Index Structures
- **B-Tree**: Keys and values are stored in all nodes.
- **B+Tree**: Values only in leaf nodes; leaves are linked for extremely fast range scans. **Standard for RDBMS.**

### 6.3 Clustered vs Non-Clustered Indexes
- **Clustered**: Tables are stored physically in the index's order. Only one per table.
- **Non-Clustered**: A separate list of pointers to the actual data rows.

### 6.4 Composite Indexes: The Leftmost Prefix Rule
- An index on `(FirstName, LastName)` can be used for searches on `FirstName` or `FirstName + LastName`, but **not** `LastName` alone.

### 6.5 What is a Covering Index?
- A Non-Clustered index that includes all the columns requested in a query (via `INCLUDE` in SQL Server). The engine never has to "look up" the main table.

### 6.6 SARGability: Writing Index-Optimized Queries
- **Search ARGument-able**. 
- **BAD**: `WHERE UPPER(Email) = 'FOO@BAR.COM'` (Function prevents index use).
- **GOOD**: `WHERE Email = 'foo@bar.com'`.

### 6.7 Full-Text Search and Specialized Indexes (GIN/GiST)
- **Full-Text**: Linguistic search (stemming, ranking).
- **GIN (Generalized Inverted Index)**: Used for arrays and JSONB containment.
- **GiST**: Used for geometric and range data.

### 6.8 Index Fragmentation and Maintenance
- Over time, page splits cause indexes to become fragmented. Regular **Rebuild** (offline/online) or **Reorganize** (low impact) is required.

[Back to Top](#table-of-contents)

---

## 7. Database Design Patterns (OLAP)

### 7.1 OLTP vs OLAP Architecture
- **OLTP (Online Transaction Processing)**: Normalized, many small writes/reads, current state.
- **OLAP (Online Analytical Processing)**: Denormalized, massive scans, historical data, aggregates.

### 7.2 Star Schema: Facts and Dimensions
- A central **Fact Table** (numbers) joined to multiple **Dimension Tables** (descriptions).
- Simplest and fastest for most BI tools.

### 7.3 Snowflake Schema: Normalized Dimensions
- Dimension tables are themselves normalized.
- Saves space but adds join complexity and can slow down query performance.

### 7.4 Fact Tables: Transactional vs Snapshot
- **Transactional**: Record every event (e.g., every single sale).
- **Periodic Snapshot**: Summarize state at intervals (e.g., end-of-day bank balance).

### 7.5 Dimension Types: Junk, Degenerate, Bridge
- **Junk**: Combine low-cardinality flags (e.g., is_active, gender) into one table.
- **Degenerate**: Storing an ID (like Invoice_No) directly in the Fact table without a dim table.
- **Bridge**: Used for Many-to-Many relationships in dimensions (e.g., one Book has many Authors).

### 7.6 SCD Types 1, 2, and 3 (Slowly Changing Dimensions)
- **Type 1**: Overwrite (e.g., fixing a typo). No history.
- **Type 2**: Add a new row with `Eff_Date` and `End_Date`. Full history tracking.
- **Type 3**: Add a "PreviousValue" column. Limited history.

[Back to Top](#table-of-contents)
