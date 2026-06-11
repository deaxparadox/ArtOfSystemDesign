# Phase 4 — Caching

Caching is the single highest-leverage performance optimization in distributed systems. A well-placed cache can reduce database load by 95%+ and cut latency from 50ms to under 1ms. But caching is also one of the hardest problems in computer science — Phil Karlton famously said there are only two hard things: cache invalidation and naming things.

## Why This Phase Matters

Without caching, almost no system can serve millions of users. But incorrect caching causes stale data, cache stampedes, and outages that are harder to debug than any database problem. This phase covers not just how to cache but how to cache *correctly*.

## Learning Path

**Timeline:** 2 weeks (~12-14 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 4.1 | [Where to Cache — Client, CDN, Server, DB Layer](./4.1-where-to-cache.md) | Cache hierarchy, browser cache, CDN, app cache, query cache | 2h |
| 4.2 | [Cache Invalidation Strategies](./4.2-cache-invalidation.md) | TTL, event-driven, write-through, stale-while-revalidate | 2-3h |
| 4.3 | [Cache Eviction Policies](./4.3-cache-eviction-policies.md) | LRU, LFU, ARC, TinyLFU, hit rate optimization | 2h |
| 4.4 | [Redis Architecture Deep Dive](./4.4-redis-architecture.md) | Event loop, data structures, persistence, Cluster, Sentinel | 2-3h |
| 4.5 | [Cache Stampede & Thundering Herd](./4.5-cache-stampede-thundering-herd.md) | Causes, mutex locking, probabilistic expiry, request coalescing | 2h |
| 4.6 | [Write-Through vs Write-Back vs Write-Around](./4.6-write-through-write-back-write-around.md) | Consistency, durability, performance, use-case decision | 2h |

## Prerequisites

- Phase 1 complete
- Phase 3 complete (especially 3.1 Relational vs NoSQL and 3.3 Replication)
- Basic understanding of key-value stores

## Phase Goals

By the end of Phase 4, you should be able to:

1. Identify the correct cache layer (client/CDN/server/DB) for a given use case
2. Choose a cache invalidation strategy and explain its consistency implications
3. Select an eviction policy (LRU vs LFU vs TinyLFU) and justify it with hit rate reasoning
4. Explain Redis single-threaded architecture and why it is fast despite being single-threaded
5. Detect and prevent cache stampede in a system design
6. Choose between write-through, write-back, and write-around for a given consistency requirement

## Navigation

| | |
|---|---|
| ⬅️ Phase 3 | [Data Storage at Scale](../phase-3/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 5 | [Messaging & Async Processing](../phase-5/README.md) |
