# Phase 3 — Data Storage at Scale

Data storage is where most distributed systems live or die. Choosing the wrong database, replication strategy, or partitioning scheme at 10K users will require a full rewrite at 10M. This phase covers the real trade-offs — not the marketing copy.

## Why This Phase Matters
Storage decisions are the hardest to undo. A wrong networking choice can be fixed in days. A wrong database choice requires months of migration. Every topic in this phase is a decision you will be held accountable for years later.

## Learning Path
**Timeline:** 2 weeks (~16-18 hours)
**Recommended pace:** 1 section per 2-3 days, with hands-on practice

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 3.1 | [Relational vs NoSQL — The Real Trade-offs](./3.1-relational-vs-nosql.md) | ACID, BASE, schema flexibility, query patterns, migration cost | 2-3h |
| 3.2 | [CAP Theorem & PACELC](./3.2-cap-theorem-pacelc.md) | Consistency, availability, partition tolerance, latency trade-offs | 2h |
| 3.3 | [Database Replication](./3.3-database-replication.md) | Leader-follower, multi-leader, leaderless, replication lag, conflicts | 2-3h |
| 3.4 | [Sharding & Partitioning Strategies](./3.4-sharding-partitioning.md) | Range, hash, directory, geo sharding, hot spots, resharding | 2-3h |
| 3.5 | [Consistent Hashing](./3.5-consistent-hashing.md) | Ring hash, virtual nodes, load distribution, cache/DB routing | 2h |
| 3.6 | [Read Replicas & Write Amplification](./3.6-read-replicas-write-amplification.md) | Read scaling, LSM vs B-tree, compaction, replication lag | 2h |
| 3.7 | [Time-Series Databases](./3.7-time-series-databases.md) | Metrics, retention, compression, InfluxDB, Prometheus, ClickHouse | 2h |
| 3.8 | [Object Storage — The S3 Model](./3.8-object-storage.md) | Eventual consistency, multipart upload, lifecycle, versioning, cost | 2h |

## Prerequisites
- Phase 1 complete (especially 1.2 Fallacies and 1.5 Stateless vs Stateful)
- Phase 2 complete (especially 2.4 Load Balancers)
- Basic SQL familiarity (SELECT, JOIN, INDEX)
- Conceptual understanding of what a database does

## Phase Goals

By the end of Phase 3, you should be able to:

1. Choose between relational and NoSQL for a given use case with a concrete reason
2. Apply CAP theorem as a decision framework — not just recite it as a fact
3. Explain replication lag and its user-visible consequences
4. Choose a sharding strategy for a given access pattern and justify it
5. Explain consistent hashing and why it reduces remapping cost vs modulo hashing
6. Explain write amplification and when it becomes a problem at scale
7. Know when to use a time-series database vs a relational database for metrics
8. Describe the S3 consistency model and design around its limitations

## Navigation

| | |
|---|---|
| ⬅️ Phase 2 | [Networking & Communication](../phase-2/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 4 | [Caching](../phase-4/README.md) |
