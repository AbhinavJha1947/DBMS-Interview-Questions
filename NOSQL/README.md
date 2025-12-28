# NoSQL Fundamentals & Distributed Databases

[← Back to DBMS Index](../README.md)

Welcome to the NoSQL Interview Questions repository. This guide covers the 4 main types of NoSQL databases, distributed system internals, and architectural patterns.

## Table of Contents

### 1. NoSQL Basics & Architecture
- 1.1 [What is NoSQL?](#11-what-is-nosql)
- 1.2 [Why use NoSQL over RDBMS? (The Motivations)](#12-why-use-nosql-over-rdbms-the-motivations)
- 1.3 [What are the 4 main types of NoSQL databases?](#13-what-are-the-4-main-types-of-nosql-databases)
- 1.4 [What is Polyglot Persistence?](#14-what-is-polyglot-persistence)
- 1.5 [Vertical Scaling (Scale-up) vs Horizontal Scaling (Scale-out)](#15-vertical-scaling-scale-up-vs-horizontal-scaling-scale-out)

### 2. Key-Value Stores (e.g., Redis, DynamoDB)
- 2.1 [What is a Key-Value Store?](#21-what-is-a-key-value-store)
- 2.2 [Use Cases for Key-Value Stores](#22-use-cases-for-key-value-stores)
- 2.3 [Redis: Data Structures and Persistence (RDB vs AOF)](#23-redis-data-structures-and-persistence-rdb-vs-aof)
- 2.4 [How does Caching strategy work (Cache-Aside, Write-Through)?](#24-how-does-caching-strategy-work-cache-aside-write-through)
- 2.5 [What is Data Expiration (TTL)?](#25-what-is-data-expiration-ttl)

### 3. Document Databases (e.g., MongoDB)
- 3.1 [What is a Document Database?](#31-what-is-a-document-database)
- 3.2 [JSON vs BSON (Binary JSON)](#32-json-vs-bson-binary-json)
- 3.3 [Data Modeling: Embedding vs Referencing](#33-data-modeling-embedding-vs-referencing)
- 3.4 [What is Schema-less (Flexible Schema)?](#34-what-is-schema-less-flexible-schema)
- 3.5 [When to chose a Document Store over a Relational Table?](#35-when-to-chose-a-document-store-over-a-relational-table)

### 4. Wide-Column Stores (e.g., Cassandra, HBase)
- 4.1 [What is a Wide-Column Store?](#41-what-is-a-wide-column-store)
- 4.2 [Row-Oriented vs Column-Family data layout](#42-row-oriented-vs-column-family-data-layout)
- 4.3 [Cassandra Architecture: The Ring, Gossip, and Snitch](#43-cassandra-architecture-the-ring-gossip-and-snitch)
- 4.4 [Use Cases: Time-Series and Write-Heavy loads](#44-use-cases-time-series-and-write-heavy-loads)

### 5. Graph Databases (e.g., Neo4j)
- 5.1 [What is a Graph Database?](#51-what-is-a-graph-database)
- 5.2 [Nodes, Edges, Properties, and Labels](#52-nodes-edges-properties-and-labels)
- 5.3 [What is Index-Free Adjacency?](#53-what-is-index-free-adjacency)
- 5.4 [Use Cases: Fraud Detection, Recommendation Engines](#54-use-cases-fraud-detection-recommendation-engines)

### 6. Distributed System Concepts (The Core)
- 6.1 [Replication: Master-Slave vs Multi-Leader vs Leaderless](#61-replication-master-slave-vs-multi-leader-vs-leaderless)
- 6.2 [Sharding (Partitioning): Range, Hash, and Directory](#62-sharding-partitioning-range-hash-and-directory)
- 6.3 [What is Consistent Hashing?](#63-what-is-consistent-hashing)
- 6.4 [Quorums (N, R, W) and Tunable Consistency](#64-quorums-n-r-w-and-tunable-consistency)
- 6.5 [Vector Clocks and Conflict Resolution](#65-vector-clocks-and-conflict-resolution)
- 6.6 [Gossip Protocol](#66-gossip-protocol)
- 6.7 [Anti-Entropy: Merkle Trees](#67-anti-entropy-merkle-trees)
- 6.8 [Hinted Handoff](#68-hinted-handoff)

### 7. Storage Engine Internals
- 7.1 [LSM Trees (Log-Structured Merge-Trees)](#71-lsm-trees-log-structured-merge-trees)
- 7.2 [SSTables (Sorted String Tables) and MemTables](#72-sstables-sorted-string-tables-and-memtables)
- 7.3 [Write Amplification vs Read Amplification](#73-write-amplification-vs-read-amplification)
- 7.4 [Bloom Filters: Optimization for Reads](#74-bloom-filters-optimization-for-reads)
- 7.5 [Comparison: LSM Trees (NoSQL) vs B-Trees (RDBMS)](#75-comparison-lsm-trees-nosql-vs-b-trees-rdbms)

---

## 1. NoSQL Basics & Architecture

### 1.1 What is NoSQL?
- Stand for **"Not Only SQL"**.
- A broad class of database management systems that differ from the classic relational model. They do not typically use SQL as their primary query language and do not guarantee ACID properties in the same way (often favoring BASE).

### 1.2 Why use NoSQL over RDBMS? (The Motivations)
- **Scalability**: Designed for horizontal scaling (adding cheap servers).
- **Flexibility**: Schema-less data models allow rapid iteration.
- **Performance**: Specialized for specific access patterns (e.g., high-throughput writes, key-based lookups).
- **Big Data**: Capable of handling petabytes of unstructured data.

### 1.3 What are the 4 main types of NoSQL databases?
1.  **Key-Value**: Simple, fast (Redis, DynamoDB).
2.  **Document**: Hierarchical data (MongoDB, Couchbase).
3.  **Wide-Column**: Massive scalability (Cassandra, HBase).
4.  **Graph**: Complex relationships (Neo4j, Amazon Neptune).

### 1.4 What is Polyglot Persistence?
- The practice of using different data storage technologies to handle different data storage needs within a given system.
- *Example*: Use MongoDB for the product catalog (flexible), Redis for the shopping cart (speed), and Neo4j for recommendations (relationships).

### 1.5 Vertical Scaling (Scale-up) vs Horizontal Scaling (Scale-out)
- **Vertical**: Adding more CPU/RAM to a single master server. RDBMS traditional limit.
- **Horizontal**: Adding more nodes to a cluster. NoSQL design goal.

[Back to Top](#table-of-contents)

---

## 2. Key-Value Stores

### 2.1 What is a Key-Value Store?
- The simplest NoSQL model. Data is stored as a collection of key-value pairs.
- The value is an opaque blob to the database; it just stores and retrieves it by key.

### 2.2 Use Cases for Key-Value Stores
- **Session Caching**: Storing user session tokens.
- **Shopping Carts**: Fast R/W for temporary data.
- **Real-time Counters**: Likes, views, leaderboards.

### 2.3 Redis: Data Structures and Persistence (RDB vs AOF)
- **Structures**: Strings, Lists, Sets, Hashes, Sorted Sets.
- **RDB (Snapshot)**: Point-in-time snapshot of dataset at intervals. Faster checks/restore, data loss possible between snaps.
- **AOF (Append Only File)**: Logs every write. Higher durability, slower recovery.

### 2.4 How does Caching strategy work (Cache-Aside, Write-Through)?
- **Cache-Aside**: App checks Cache. If miss, reads DB, then writes to Cache.
- **Write-Through**: App writes to Cache, Cache writes to DB. Data always consistent/fresh.

### 2.5 What is Data Expiration (TTL)?
- **Time To Live**: Automatically deleting keys after a set time (e.g., sessions expire after 30 mins).

[Back to Top](#table-of-contents)

---

## 3. Document Databases

### 3.1 What is a Document Database?
- Stores data in documents (JSON/XML) rather than rows.
- Documents are grouped into Collections (Tables).
- Key feature: **Schema Flexibility**. Different documents in the same collection can have different fields.

### 3.2 JSON vs BSON (Binary JSON)
- **JSON**: Text-based, human readable.
- **BSON**: Binary-encoded serialization of JSON-like documents. Used by MongoDB.
    - Adds types (Date, Byte Array).
    - Optimizes scan speed (length prefixes) and traversal.

### 3.3 Data Modeling: Embedding vs Referencing
- **Embedding (Denormalization)**: Storing related data in a single document.
    - *Pro*: One read to get everything. Atomic update.
    - *Con*: Document size limit (16MB in Mongo), data duplication.
- **Referencing (Normalization)**: Storing ID references to other documents.
    - *Pro*: No duplication, smaller docs.
    - *Con*: Application-level joins (slower).

### 3.4 What is Schema-less (Flexible Schema)?
- No DDL required to add fields. 
- Application code manages the schema (Schema-on-Read).

### 3.5 When to chose a Document Store over a Relational Table?
- When data is hierarchical or deeply nested.
- When requirements/schema change frequently.
- For Content Management Systems (CMS) or Catalogs.

[Back to Top](#table-of-contents)

---

## 4. Wide-Column Stores

### 4.1 What is a Wide-Column Store?
- Evolution of Google BigTable.
- Stores data in **Column Families**. Key -> Column Family -> Column Qualifier -> Value.
- Imagine a map of maps. Highly sparse: rows can have millions of columns.

### 4.2 Row-Oriented vs Column-Family data layout
- **Row-Store (RDBMS)**: `(ID, Name, Age)` stored contiguously. Good for fetching whole records.
- **Column-Family**: All values for specific columns are stored together on disk. Good for writing massive throughput and compression.

### 4.3 Cassandra Architecture: The Ring, Gossip, and Snitch
- **Ring**: Peer-to-peer ring topology. No single master.
- **Gossip Protocol**: Nodes periodically exchange state info with peers to discover failure/topology changes.
- **Snitch**: Tells Cassandra which datacenter/rack a node belongs to for replication awareness.

### 4.4 Use Cases: Time-Series and Write-Heavy loads
- IoT sensor data (massive write ingestion).
- Chat message history (Facebook Messenger uses HBase/Cassandra).
- Metrics/Logging.

[Back to Top](#table-of-contents)

---

## 5. Graph Databases

### 5.1 What is a Graph Database?
- Optimized for traversing relationships.
- Uses **Graph Theory** objects: Nodes and Edges.

### 5.2 Nodes, Edges, Properties, and Labels
- **Node**: Entity (Person, Place).
- **Edge**: Relationship (KNOWS, BOUGHT, LIVES_IN). Directed and typed.
- **Properties**: Key-values stored on both nodes and edges (e.g., `since: 2023` on a KNOWS edge).

### 5.3 What is Index-Free Adjacency?
- Each node physically contains pointers to its neighbors.
- Traversal is `O(k)` (where k is neighbors), not `O(log N)` like B-Tree joins. This means performance is constant regardless of total dataset size.

### 5.4 Use Cases: Fraud Detection, Recommendation Engines
- "People who bought X also bought Y".
- Finding fraud rings (circular money transfers).

[Back to Top](#table-of-contents)

---

## 6. Distributed System Concepts (The Core)

### 6.1 Replication: Master-Slave vs Multi-Leader vs Leaderless
- **Master-Slave (Primary-Secondary)**: Writes to Master, Reads from Slaves. Async replication. Risk: Stale reads.
- **leaderless (Dynamo-style)**: Client writes to any node. Coordinator forwards. Used by Cassandra. High availability.

### 6.2 Sharding (Partitioning): Range, Hash, and Directory
- **Range**: Split by Key Range (A-M, N-Z). Good for range scans. Bad for hotspots (e.g., time-based).
- **Hash**: Hash(Key) % N. Distributes evenly. No range scans.
- **Directory**: Lookup service points to the shard.

### 6.3 What is Consistent Hashing?
- A technique to distribute keys across a ring of nodes such that adding/removing a node only affects `K/n` keys (neighbors).
- Minimizes data movement during scaling.

### 6.4 Quorums (N, R, W) and Tunable Consistency
- Used in Leaderless systems.
- **N**: Replication factor (e.g., 3).
- **R**: Read quorum (nodes needed to confirm read).
- **W**: Write quorum (nodes needed to confirm write).
- **Strong Consistency**: If `R + W > N`.

### 6.5 Vector Clocks and Conflict Resolution
- In distributed systems (AP), concurrent writes happen.
- **Vector Clocks**: Metadata (`NodeA:1, NodeB:2`) attached to data to track causality and detect conflicts (siblings) that must be resolved by the app (LWW - Last Write Wins is simpler alternative).

### 6.6 Gossip Protocol
- Epidemic protocol. Nodes infect neighbors with information. State spreads exponentially fast across the cluster.

### 6.7 Anti-Entropy: Merkle Trees
- How nodes check if their data is in sync.
- **Merkle Tree**: Hash tree. Root hash compares entire dataset. If different, traverse down to find exact different block. Saves bandwidth.

### 6.8 Hinted Handoff
- If a node is down, the coordinator holds the write "hint" and replays it when the node comes back online.

[Back to Top](#table-of-contents)

---

## 7. Storage Engine Internals

### 7.1 LSM Trees (Log-Structured Merge-Trees)
- The write-optimized structure used by Cassandra, RocksDB, HBase.
- Writes go into memory -> flushed to immutable disk files -> merged later.
- Transforms random writes into sequential writes.

### 7.2 SSTables (Sorted String Tables) and MemTables
- **MemTable**: In-memory mutable buffer (Red-Black Tree or Skip List).
- **SSTable**: Immutable on-disk file. Keys are sorted.

### 7.3 Write Amplification vs Read Amplification
- **Write Amp**: One user write = multiple disk writes (WAL, MemTable flush, Compaction).
- **Read Amp**: One user read = checking MemTable + multiple SSTables.

### 7.4 Bloom Filters: Optimization for Reads
- A probabilistic data structure to tell if an element is *definitely not* in a set.
- Used to avoid checking SSTables that don't contain the key.

### 7.5 Comparison: LSM Trees (NoSQL) vs B-Trees (RDBMS)
- **LSM**: Faster Writes (Append-only). Slower Reads (Check levels). High compression.
- **B-Tree**: Faster Reads (Single seek). Slower Writes (In-place update, fragmentation).

[Back to Top](#table-of-contents)
