# The Art of System Design

A structured, opinionated curriculum for learning large-scale distributed systems — built for engineers who want to go from "I've heard of Kafka" to "I can defend this architecture decision with numbers."

This is not a collection of blog summaries. Every topic is grounded in real production decisions, real failure post-mortems, and real trade-offs with specific numbers attached.

---

## How to Use This

**Learning path:** Follow the phases in order. Phase 2 is where 80% of interview material lives — do not skip to Phase 4 because it sounds more impressive.

**Pattern that works:** concept → diagram → practice problem → real case study → repeat. Reading without designing is how engineers stay stuck.

**Using the teach skill:** In any Claude Code session, invoke `/teach-system-design:teach [topic]` for a deep-dive on any topic in the roadmap. Use `/teach-system-design:test` for quizzes and design challenges.

**Recommended pace:** 2–3 topics per week. Phase 10 (Classic Problems) should be done after all prior phases — not as a shortcut.

---

## Table of Contents

- [Curriculum Roadmap](#curriculum-roadmap)
- [Phase 1 — Foundations of Distributed Systems](#phase-1--foundations-of-distributed-systems)
- [Phase 2 — Networking & Communication](#phase-2--networking--communication)
- [Phase 3 — Data Storage at Scale](#phase-3--data-storage-at-scale)
- [Phase 4 — Caching](#phase-4--caching)
- [Phase 5 — Messaging & Async Processing](#phase-5--messaging--async-processing)
- [Phase 6 — Scalability Patterns](#phase-6--scalability-patterns)
- [Phase 7 — Microservices & Service Architecture](#phase-7--microservices--service-architecture)
- [Phase 8 — Reliability & Operations](#phase-8--reliability--operations)
- [Phase 9 — Security at Scale](#phase-9--security-at-scale)
- [Phase 10 — Classic System Design Problems](#phase-10--classic-system-design-problems)
- [Numbers Every Engineer Must Know](#numbers-every-engineer-must-know)
- [Technology Comparisons](#technology-comparisons)
- [Real-World Case Studies](#real-world-case-studies)
- [Interview Preparation](#interview-preparation)
- [External Resources](#external-resources)

---

## Curriculum Roadmap

```
PHASE 1 — Foundations of Distributed Systems          [Weeks 1–2]
  → See: phase-1/ directory for full content
  1.1  What is a distributed system?
  1.2  The 8 Fallacies of Distributed Computing
  1.3  Latency vs throughput
  1.4  Horizontal vs vertical scaling
  1.5  Stateless vs stateful systems
  1.6  SLAs, SLOs, SLIs — what they actually mean

PHASE 2 — Networking & Communication                   [Weeks 3–4]
  2.1  TCP vs UDP — when each matters
  2.2  HTTP/1.1 vs HTTP/2 vs HTTP/3
  2.3  DNS and how it affects architecture
  2.4  Load balancers (L4 vs L7)
  2.5  Reverse proxies
  2.6  CDNs — how they work and when to use them
  2.7  Long polling, SSE, WebSockets

PHASE 3 — Data Storage at Scale                        [Weeks 5–6]
  3.1  Relational vs NoSQL — the real trade-offs
  3.2  CAP theorem & PACELC
  3.3  Database replication (leader-follower, multi-leader, leaderless)
  3.4  Sharding & partitioning strategies
  3.5  Consistent hashing
  3.6  Read replicas & write amplification
  3.7  Time-series databases
  3.8  Object storage (S3 model)

PHASE 4 — Caching                                      [Weeks 7–8]
  4.1  Where to cache: client, CDN, server, DB layer
  4.2  Cache invalidation strategies
  4.3  Cache eviction policies (LRU, LFU, etc.)
  4.4  Redis architecture deep dive
  4.5  Cache stampede & thundering herd problem
  4.6  Write-through vs write-back vs write-around

PHASE 5 — Messaging & Async Processing                 [Weeks 9–10]
  5.1  Why async? The producer-consumer model
  5.2  Message queues vs event streams
  5.3  Kafka architecture & guarantees
  5.4  RabbitMQ vs Kafka vs SQS
  5.5  At-least-once vs exactly-once delivery
  5.6  Dead letter queues
  5.7  Backpressure & flow control

PHASE 6 — Scalability Patterns                         [Weeks 11–12]
  6.1  The 12-Factor App
  6.2  Rate limiting (token bucket, leaky bucket, sliding window)
  6.3  Circuit breakers & bulkheads
  6.4  Retry strategies with exponential backoff
  6.5  Idempotency
  6.6  Saga pattern for distributed transactions
  6.7  CQRS & Event Sourcing
  6.8  Fan-out on write vs fan-out on read

PHASE 7 — Microservices & Service Architecture         [Weeks 13–14]
  7.1  Monolith vs microservices — honest trade-offs
  7.2  Service discovery
  7.3  API gateways
  7.4  Service meshes (Istio, Linkerd)
  7.5  Inter-service communication: REST vs gRPC vs events
  7.6  Distributed tracing
  7.7  When to use a monolith (this matters more than people admit)

PHASE 8 — Reliability & Operations                     [Weeks 15–16]
  8.1  Fault tolerance — what it actually means
  8.2  Replication & redundancy
  8.3  Chaos engineering
  8.4  Health checks, readiness vs liveness probes
  8.5  Graceful degradation
  8.6  Disaster recovery: RPO vs RTO
  8.7  Incident management & post-mortems

PHASE 9 — Security at Scale                            [Weeks 17–18]
  9.1  Authentication at scale (OAuth2, OIDC, JWT)
  9.2  Zero-trust architecture
  9.3  API security: rate limiting, input validation, secrets
  9.4  DDoS mitigation patterns
  9.5  mTLS in service meshes

PHASE 10 — Classic System Design Problems              [Weeks 19–26]
  10.1  Design a URL shortener
  10.2  Design a rate limiter
  10.3  Design a notification system
  10.4  Design a social feed / timeline (Twitter/Instagram model)
  10.5  Design a chat system (WhatsApp model)
  10.6  Design a search autocomplete
  10.7  Design a distributed cache
  10.8  Design a file storage system (Dropbox/S3 model)
  10.9  Design a ride-sharing service (Uber model)
  10.10 Design a video streaming platform (YouTube model)
```

---

## Phase 1 — Foundations of Distributed Systems

**[→ Full Phase 1 Learning Materials](./phase-1/README.md)**

**Why this phase matters:** Everything in Phases 2–10 is a specific solution to a problem created by distribution. If you don't understand the fundamental problems, the solutions feel like arbitrary trivia.

### [1.1 What is a Distributed System?](./phase-1/1.1-what-is-a-distributed-system.md)

A system where multiple computers coordinate to appear as a single system to users. The moment you need two machines, you have a distributed system — and a whole new class of failures.

The core problem: **partial failure**. In a single machine, it either works or crashes. In a distributed system, some parts can fail while others continue. A request can be sent but the response lost. A write can succeed on one node but not another. The system must decide what to do in each case.

### [1.2 The 8 Fallacies of Distributed Computing](./phase-1/1.2-eight-fallacies.md)

Peter Deutsch's list of assumptions that will cause your distributed system to fail in production:

1. The network is reliable
2. Latency is zero
3. Bandwidth is infinite
4. The network is secure
5. Topology doesn't change
6. There is one administrator
7. Transport cost is zero
8. The network is homogeneous

Every fallacy is an assumption baked into "it works on my laptop" architectures that breaks at scale.

### [1.3 Latency vs Throughput](./phase-1/1.3-latency-vs-throughput.md)

- **Latency:** Time to complete one operation (ms). What users feel.
- **Throughput:** Operations completed per unit of time (req/s). What systems need.
- **The tension:** Optimizing for throughput (batching, queuing) often increases latency. Optimizing for latency (synchronous, eager processing) often reduces throughput.

Rule of thumb: for interactive user-facing systems, optimize latency first. For data pipelines, optimize throughput first.

### [1.4 Horizontal vs Vertical Scaling](./phase-1/1.4-horizontal-vs-vertical-scaling.md)

- **Vertical (scale up):** Bigger machine. Simpler, but has a ceiling. CPU/RAM limits per machine are ~96 cores / 12TB RAM (2025 AWS).
- **Horizontal (scale out):** More machines. No theoretical ceiling, but requires your application to be stateless or partition-aware.

The wrong instinct: always throw horizontal scaling at a problem. The right instinct: vertical scale first until it hurts, then design for horizontal. Premature horizontal scaling is a major source of operational complexity.

### [1.5 Stateless vs Stateful Systems](./phase-1/1.5-stateless-vs-stateful.md)

- **Stateless:** Every request contains all information needed to process it. Any instance can handle any request. Easy to scale horizontally, restart, and replace.
- **Stateful:** State lives in the server. Requests must be routed to the correct instance (session affinity / sticky sessions). Harder to scale, but sometimes unavoidable (WebSocket connections, game servers).

Design principle: push state to the edges (databases, caches, queues). Keep your application servers stateless.

### [1.6 SLAs, SLOs, SLIs](./phase-1/1.6-slas-slos-slis.md)

- **SLI (Service Level Indicator):** The measurement. E.g., "p99 API response time."
- **SLO (Service Level Objective):** The target. E.g., "p99 < 200ms over a 30-day window."
- **SLA (Service Level Agreement):** The contract with consequences. E.g., "If we miss the SLO, you get a 10% credit."

The common mistake: setting SLAs without SLOs. SLOs without SLIs are just wishful thinking — you need the measurement before you can set the target.

Google's Site Reliability Engineering (SRE) book is the canonical reference for this. The concept of **error budgets** (the acceptable amount of downtime before violating an SLO) is critical.

---

## Phase 2 — Networking & Communication

**[→ Full Phase 2 Learning Materials](./phase-2/README.md)**

### [2.1 TCP vs UDP](./phase-2/2.1-tcp-vs-udp.md)

| Property | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery, ordering | No guarantees |
| Error handling | Retransmission built-in | Application handles or ignores |
| Overhead | ~20-byte header + handshake | ~8-byte header |
| Speed | Slower (ack required) | Faster |
| Use cases | HTTP, databases, SSH, file transfer | DNS, gaming, video streaming, VoIP |

**The real decision:** TCP when losing data is unacceptable. UDP when losing a packet is better than waiting for retransmission (live video: a dropped frame is better than a 200ms stall).

### [2.2 HTTP/1.1 vs HTTP/2 vs HTTP/3](./phase-2/2.2-http-versions.md)

| Property | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| Transport | TCP | TCP | QUIC (UDP) |
| Multiplexing | No (one req/connection, or pipelining with HOL blocking) | Yes (streams) | Yes (streams, no HOL blocking) |
| Header compression | None | HPACK | QPACK |
| Server push | No | Yes | Yes |
| TLS | Optional | Effectively required | Required |
| Latency improvement | Baseline | ~50% improvement | ~30% over HTTP/2, especially on lossy networks |

HTTP/3's killer feature: no head-of-line blocking at the transport layer. In HTTP/2, a single lost TCP packet stalls all streams on the connection. HTTP/3's QUIC protocol handles each stream independently at the transport layer.

### [2.3 DNS and How It Affects Architecture](./phase-2/2.3-dns.md)

### [2.4 Load Balancers: L4 vs L7](./phase-2/2.4-load-balancers.md)

```
L4 (Transport Layer)                L7 (Application Layer)
─────────────────────────────────   ───────────────────────────────────
Routes by IP + port only            Routes by URL, headers, cookies
No TLS termination (pass-through)   TLS termination
Sub-millisecond latency             Slightly higher latency
AWS: NLB                            AWS: ALB, Nginx, Envoy, HAProxy
Use: low-latency, non-HTTP          Use: HTTP microservices, A/B testing
```

**Load balancing algorithms:**

| Algorithm | Best For | Pitfall |
|---|---|---|
| Round-robin | Homogeneous, stateless | Bad when requests have variable cost |
| Least connections | Variable request duration | Doesn't account for request cost |
| Consistent hashing | Cache affinity, sticky sessions | Uneven distribution with few nodes |
| IP hash | Simple session affinity | Breaks behind NAT (all users same IP) |

### [2.5 Reverse Proxies](./phase-2/2.5-reverse-proxies.md)

### [2.6 CDNs](./phase-2/2.6-cdns.md)

A CDN is a globally distributed network of edge servers that cache content closer to users.

**How it works:**
1. User requests `image.example.com/photo.jpg`
2. DNS resolves to nearest CDN edge (anycast routing)
3. Cache HIT → response in <20ms from edge
4. Cache MISS → edge fetches from origin, caches, returns response

**Cache-Control headers are the real CDN API:**
```
Cache-Control: public, max-age=86400          # Cache 24h at CDN + browser
Cache-Control: public, s-maxage=3600          # Cache 1h at CDN only
Cache-Control: no-cache                       # Always revalidate
Cache-Control: no-store                       # Never cache (PII, auth)
```

**When CDNs fail you:** Dynamic content that can't be cached (personalized feeds, auth-gated content). For this, CDN acts as a reverse proxy only — you get DDoS protection and TLS termination but no cache benefit.

### [2.7 Real-time Communication](./phase-2/2.7-realtime-communication.md)

| Pattern | Latency | Direction | Best For | Overhead |
|---|---|---|---|---|
| Long polling | 100–500ms | Server → Client | Simple notifications, fallback | High (repeated connections) |
| Server-Sent Events (SSE) | <50ms | Server → Client only | Live feeds, dashboards | Low |
| WebSockets | <10ms | Bidirectional | Chat, gaming, collaborative editing | Medium (persistent connection) |
| gRPC streaming | <10ms | Bidirectional | Internal microservices | Low (binary protocol) |

**WebSocket connection cost at scale:** Each open WebSocket is a persistent TCP connection. At 1M concurrent users, that's 1M open file descriptors per server. Linux default limit is 1024 — this must be tuned (`ulimit -n 1000000`, `net.ipv4.tcp_fin_timeout`, etc.). Discord handles millions of concurrent WebSocket connections per server by tuning these limits and using Rust/Elixir for connection handling.

---

## Phase 3 — Data Storage at Scale

**[→ Full Phase 3 Learning Materials](./phase-3/README.md)**

### [3.1 Relational vs NoSQL — The Real Trade-offs](./phase-3/3.1-relational-vs-nosql.md)

**The real decision framework** (not "SQL for structured data, NoSQL for unstructured"):

Use **PostgreSQL** when:
- You need multi-row ACID transactions
- Data relationships require joins
- Your query patterns are unpredictable (ad-hoc reporting)
- Team is small and operational simplicity matters

Use **Cassandra / DynamoDB** when:
- Write throughput > 50K writes/sec sustained
- Data can be modeled as key-value or wide-column with known access patterns
- Geo-distribution and multi-master writes are required
- You can tolerate eventual consistency

Use **MongoDB** when:
- Document model fits your data (nested objects, flexible schema)
- You need to iterate schema quickly (early product stage)
- Read-heavy with simple queries by document ID

**Opinionated guidance:** Start with PostgreSQL. It handles more workloads than people expect. Move to NoSQL when you have a *specific, measured* scaling problem — not as a first choice.

### [3.2 CAP Theorem & PACELC](./phase-3/3.2-cap-theorem-pacelc.md)

CAP says a distributed system can guarantee at most 2 of:
- **Consistency (C):** Every read sees the most recent write
- **Availability (A):** Every request gets a response (may not be the latest data)
- **Partition tolerance (P):** System continues operating when network partitions occur

Because network partitions are a fact of distributed systems (not optional), the real choice is **CP vs AP**:

- **CP (choose consistency over availability):** During a partition, refuse requests rather than return stale data. E.g., HBase, ZooKeeper, etcd. Use for financial systems, inventory.
- **AP (choose availability over consistency):** During a partition, return potentially stale data. E.g., Cassandra, DynamoDB, CouchDB. Use for social feeds, analytics.

**PACELC** extends CAP for normal operation: even without partitions, there's a trade-off between Latency and Consistency. Cassandra is PA/EL (high availability, low latency, eventual consistency). PostgreSQL is PC/EC (consistent, higher latency).

### [3.3 Database Replication](./phase-3/3.3-database-replication.md)

### [3.4 Sharding & Partitioning Strategies](./phase-3/3.4-sharding-partitioning.md)

| Strategy | How It Works | Best For | Pitfall |
|---|---|---|---|
| Range-based | Key ranges → shards (A-M, N-Z) | Sequential reads, range queries | Hot spots if data isn't evenly distributed |
| Hash-based | hash(key) % N → shard | Even distribution | Range queries require scatter-gather |
| Directory-based | Lookup table maps keys to shards | Flexible, easy resharding | Lookup table becomes bottleneck |
| Geo-based | User region → shard | Regulatory compliance, latency | Uneven shard sizes across regions |

### [3.5 Consistent Hashing](./phase-3/3.5-consistent-hashing.md)

The problem with `hash(key) % N`: when you add or remove a node, almost all keys remap (N/(N+1) ≈ 100% remapping).

Consistent hashing solution: place both nodes and keys on a ring (0 to 2^32). Each key is served by the first node clockwise from its position. When a node is added/removed, only the keys between it and its predecessor remap — average N/N+1 keys, not all of them.

**Virtual nodes:** A single physical node maps to multiple positions on the ring (e.g., 100–200 virtual nodes per physical). This prevents hot spots when nodes have different capacities and handles uneven distribution.

Used by: Cassandra, DynamoDB, Redis Cluster, Memcached client libraries.

### [3.6 Read Replicas & Write Amplification](./phase-3/3.6-read-replicas-write-amplification.md)

### [3.7 Time-Series Databases](./phase-3/3.7-time-series-databases.md)

### [3.8 Object Storage — The S3 Model](./phase-3/3.8-object-storage.md)

---

## Phase 4 — Caching

**[→ Full Phase 4 Learning Materials](./phase-4/README.md)**

### [4.1 Where to Cache](./phase-4/4.1-where-to-cache.md)

### Cache Impact on Latency

Assuming 1ms cache hit vs 50ms database read:

| Cache Hit Rate | Average Latency |
|---|---|
| 80% | 10.8ms |
| 90% | 5.9ms |
| 95% | 3.5ms |
| 99% | 1.5ms |
| 99.9% | 1.05ms |

**The delta between 95% and 99% is 2x latency improvement.** This is why cache hit rate is a critical operational metric to track — a 4% change has massive user-facing impact.

### [4.2 Cache Invalidation Strategies](./phase-4/4.2-cache-invalidation.md)

| Strategy | How | When to Use | Risk |
|---|---|---|---|
| TTL (Time-to-live) | Keys expire after N seconds | Tolerable eventual consistency | Stale data up to TTL duration |
| Write-through | Update cache on every write | Consistency critical, write-heavy | Higher write latency |
| Write-back (write-behind) | Write to cache, async flush to DB | Write-heavy, can tolerate data loss | Data loss on cache crash |
| Cache-aside (lazy loading) | App reads DB on miss, populates cache | Read-heavy, unpredictable access | Cache stampede on cold start |
| Event-driven invalidation | Subscribe to change events, evict keys | Strong consistency without TTL penalty | Complex infrastructure |

### [4.3 Cache Eviction Policies](./phase-4/4.3-cache-eviction-policies.md)

### [4.4 Redis Architecture Deep Dive](./phase-4/4.4-redis-architecture.md)

### [4.5 Cache Stampede & Thundering Herd](./phase-4/4.5-cache-stampede-thundering-herd.md)

**The problem:** A popular key expires. 10,000 concurrent requests all get a cache miss simultaneously. All 10,000 go to the database at once. The database falls over. The cache never gets repopulated. The system enters a death spiral.

**Solutions:**
1. **Mutex/lock on miss:** First request to miss acquires a lock, fetches from DB, populates cache. Others wait. Works but adds latency.
2. **Probabilistic early expiration:** When a key is `X` seconds from expiry, probabilistically refresh early with probability proportional to `time_to_expiry`. Spreads recomputation over time.
3. **Background refresh:** Always serve potentially stale data; refresh in background asynchronously before expiry.
4. **Request coalescing:** (What Discord's Rust service does) Deduplicate concurrent requests for the same key — 1,000 concurrent requests for the same `channel_id` → 1 database query, 1 cache write, 1,000 waiters unblocked.

### [4.6 Write-Through vs Write-Back vs Write-Around](./phase-4/4.6-write-through-write-back-write-around.md)

---

## Phase 5 — Messaging & Async Processing

**[→ Full Phase 5 Learning Materials](./phase-5/README.md)**

### [5.1 Why Async? The Producer-Consumer Model](./phase-5/5.1-why-async-producer-consumer.md)

### [5.2 Message Queues vs Event Streams](./phase-5/5.2-message-queues-vs-event-streams.md)

### [5.3 Kafka Architecture & Guarantees](./phase-5/5.3-kafka-architecture.md)

```
Producer → [Topic: orders]
              Partition 0: [msg1, msg2, msg3, ...]   ← Consumer Group A (offset: 3)
              Partition 1: [msg1, msg2, ...]          ← Consumer Group A (offset: 2)
              Partition 2: [msg1, msg2, msg3, msg4]   ← Consumer Group A (offset: 4)
                                    ↑
                        Consumer Group B (independent offsets)
```

Key properties:
- **Partitions** are the unit of parallelism. N partitions → max N consumers in a group.
- **Offsets** are committed by consumers. Kafka doesn't delete messages on read — consumers track their own position.
- **Retention** is time/size based (default 7 days), not ACK-based. This enables replay.
- **Replication factor** (typically 3): each partition is replicated to 3 brokers. Failure of 1 broker is transparent.

**Kafka throughput:** LinkedIn's own benchmark: **2 million writes/second** on 3 commodity machines (6x 7200 RPM SATA, 2x quad-core Xeon). At this point, Kafka is typically the fastest component in the system.

### [5.4 RabbitMQ vs Kafka vs SQS](./phase-5/5.4-rabbitmq-vs-kafka-vs-sqs.md)

### [5.5 At-Least-Once vs Exactly-Once Delivery](./phase-5/5.5-delivery-guarantees.md)

| Guarantee | What It Means | Use When |
|---|---|---|
| At-most-once | May lose messages, no duplicates | Log aggregation, metrics |
| At-least-once | No data loss, may deliver duplicates | Most use cases — make consumers idempotent |
| Exactly-once | No loss, no duplicates | Financial transactions, inventory |

**Exactly-once is expensive:** In Kafka, it requires idempotent producers + transactional APIs + compatible consumer logic. Use at-least-once with idempotent consumers as a pragmatic default — it's simpler and the performance is significantly better.

### [5.6 Dead Letter Queues](./phase-5/5.6-dead-letter-queues.md)

### [5.7 Backpressure & Flow Control](./phase-5/5.7-backpressure-flow-control.md)

---

## Phase 6 — Scalability Patterns

**[→ Full Phase 6 Learning Materials](./phase-6/README.md)**

### [6.1 The 12-Factor App](./phase-6/6.1-twelve-factor-app.md)

### [6.2 Rate Limiting](./phase-6/6.2-rate-limiting.md)

Rate Limiting Algorithms

| Algorithm | How It Works | Burst Handling | Memory | Best For |
|---|---|---|---|---|
| Token bucket | Tokens added at fixed rate, consumed per request | Allows burst (up to bucket size) | O(1) per user | API rate limiting — most common |
| Leaky bucket | Requests enter queue, processed at fixed rate | Smooths bursts (queue) | O(queue size) | Output rate control |
| Fixed window | Count requests in fixed time window | Burst at window boundary | O(1) per user | Simple, predictable limits |
| Sliding window log | Store timestamps of all requests | Precise, no boundary burst | O(limit) per user | Strict accuracy required |
| Sliding window counter | Interpolate between two fixed windows | Near-precise with O(1) space | O(1) per user | Production default |

**Implementation:** Redis is the standard backend for distributed rate limiting. `INCR` + `EXPIRE` for simple counters; sorted sets for sliding window log.

### [6.3 Circuit Breakers & Bulkheads](./phase-6/6.3-circuit-breakers-bulkheads.md)

```
           CLOSED (normal)
           ↑         |
       success    failure threshold
           |         ↓
        HALF-OPEN ← OPEN (reject fast)
        (probe)       |
                   timeout
```

States:
- **Closed:** Requests flow normally. Track failure rate.
- **Open:** Failures exceeded threshold. Reject all requests immediately (fail fast). Wait for timeout.
- **Half-open:** Allow a single probe request. Success → close. Failure → open again.

**Why it matters:** Without circuit breakers, a struggling downstream service will exhaust your thread pool/connection pool as threads pile up waiting for timeouts. The circuit breaker converts slow failures into fast failures, preserving resources for other requests.

### [6.4 Retry Strategies with Exponential Backoff](./phase-6/6.4-retry-exponential-backoff.md)

### [6.5 Idempotency](./phase-6/6.5-idempotency.md)

### [6.6 Saga Pattern for Distributed Transactions](./phase-6/6.6-saga-pattern.md)

Distributed transactions across multiple services can't use a two-phase commit (too slow, too fragile). The Saga pattern breaks a distributed transaction into a sequence of local transactions, each with a compensating transaction for rollback.

```
Order saga:
  1. Reserve inventory       → compensate: release inventory
  2. Charge payment          → compensate: issue refund
  3. Schedule fulfillment    → compensate: cancel fulfillment
  4. Send confirmation email → no compensation needed (best-effort)
```

**Choreography vs Orchestration:**
- **Choreography:** Services react to events published by each other. Decoupled, but hard to trace and debug.
- **Orchestration:** A central saga orchestrator calls each service step. Easier to trace, single point of failure.

### [6.7 CQRS & Event Sourcing](./phase-6/6.7-cqrs-event-sourcing.md)

### [6.8 Fan-out on Write vs Fan-out on Read](./phase-6/6.8-fan-out-write-vs-read.md)

The classic example: Twitter's timeline.

**Fan-out on write (push model):** When a user tweets, immediately write to all followers' timeline caches.
- Read: O(1) — just read the pre-built timeline
- Write: O(followers) — 1 tweet from a user with 30M followers = 30M writes
- Problem: celebrities make this unsustainable

**Fan-out on read (pull model):** When a user opens their timeline, fetch recent tweets from all followees and merge.
- Read: O(followees) — slow for users following thousands of accounts
- Write: O(1) — just write the tweet once
- Problem: read latency is high for active users

**Twitter's hybrid solution:** Fan-out on write for normal users (< N followers), fan-out on read for celebrities (> N followers). Merge the two at read time. Covers 99% of users with O(1) reads while capping write amplification for high-follower accounts.

---

## Phase 7 — Microservices & Service Architecture

**[→ Full Phase 7 Learning Materials](./phase-7/README.md)**

### [7.1 Monolith vs Microservices](./phase-7/7.1-monolith-vs-microservices.md)

The honest trade-off table:

| Dimension | Monolith | Microservices |
|---|---|---|
| Deploy complexity | Low — one artifact | High — N services, N pipelines |
| Development speed (early) | Fast — no network calls | Slow — contracts, stubs, integration tests |
| Development speed (at scale) | Slow — merge conflicts, coupling | Fast — teams own services independently |
| Debugging | Easy — single process, full stack traces | Hard — distributed tracing required |
| Scaling | All-or-nothing | Per-service scaling |
| Failure isolation | None — one bug can crash all | Strong — failures are contained |
| Operational cost | Low | High — service mesh, observability, on-call |
| When to use | < 50 engineers, < 5 years old | > 100 engineers, clear domain boundaries |

**The #1 mistake:** Moving to microservices before you understand your domain boundaries. Uber's DOMA framework addresses this: group services into domains (Infrastructure → Business → Product → Presentation → Edge), with cross-layer calls as explicit contracts. Without this, you get 1,000 microservices with no ownership.

**WhatsApp benchmark:** 450M users, 50 engineers. The efficiency case for monoliths (or near-monoliths) at serious scale.

### [7.2 Service Discovery](./phase-7/7.2-service-discovery.md)

### [7.3 API Gateways](./phase-7/7.3-api-gateways.md)

### [7.4 Service Meshes](./phase-7/7.4-service-meshes.md)

### [7.5 Inter-Service Communication](./phase-7/7.5-inter-service-communication.md)

### [7.6 Distributed Tracing](./phase-7/7.6-distributed-tracing.md)

### [7.7 When to Use a Monolith](./phase-7/7.7-when-to-use-monolith.md)

---

## Phase 8 — Reliability & Operations

**[→ Full Phase 8 Learning Materials](./phase-8/README.md)**

### [8.1 Fault Tolerance — What It Actually Means](./phase-8/8.1-fault-tolerance.md)

### [8.2 Replication & Redundancy](./phase-8/8.2-replication-redundancy.md)

### [8.3 Chaos Engineering](./phase-8/8.3-chaos-engineering.md)

### [8.4 Health Checks — Readiness vs Liveness Probes](./phase-8/8.4-health-checks-probes.md)

### [8.5 Graceful Degradation](./phase-8/8.5-graceful-degradation.md)

### [8.6 Disaster Recovery: RPO vs RTO](./phase-8/8.6-disaster-recovery-rpo-rto.md)

- **RPO (Recovery Point Objective):** How much data can you afford to lose? If RPO = 1 hour, your backup strategy must run at least hourly.
- **RTO (Recovery Time Objective):** How long can the system be down? If RTO = 15 minutes, your recovery procedure must complete in 15 minutes.

| Tier | RPO | RTO | Strategy |
|---|---|---|---|
| Mission critical (payments) | ~0 | < 1 min | Multi-region active-active, synchronous replication |
| Business critical (user auth) | < 5 min | < 15 min | Cross-AZ standby, async replication |
| Important (reporting) | < 1 hour | < 4 hours | Daily snapshots, restore from backup |
| Non-critical (audit logs) | < 24 hours | < 24 hours | Daily backup, manual restore |

### [8.7 Incident Management & Post-Mortems](./phase-8/8.7-incident-management-postmortems.md)

---

## Phase 9 — Security at Scale

**[→ Full Phase 9 Learning Materials](./phase-9/README.md)**

### [9.1 Authentication at Scale — OAuth2, OIDC, JWT](./phase-9/9.1-authentication-oauth2-oidc-jwt.md)

### [9.2 Zero-Trust Architecture](./phase-9/9.2-zero-trust-architecture.md)

### [9.3 API Security](./phase-9/9.3-api-security.md)

### [9.4 DDoS Mitigation Patterns](./phase-9/9.4-ddos-mitigation.md)

### [9.5 mTLS in Service Meshes](./phase-9/9.5-mtls-service-meshes.md)

---

## Phase 10 — Classic System Design Problems

### Approach Template (use for every problem)

**Step 1 — Clarify (5 min):**
Before drawing anything, ask:
- What scale? (users, requests/sec, data volume)
- Read-heavy or write-heavy?
- Consistency requirements? (strong, eventual)
- Latency SLAs?
- Geographic distribution?
- Any specific constraints? (cost, existing infrastructure)

**Step 2 — Capacity Estimation (5 min):**
Back-of-envelope math:
- Requests per second
- Storage needed (now and 5 years out)
- Bandwidth required
- Cache sizing

**Step 3 — High-Level Design (15 min):**
5–7 boxes, arrows, and a narrated rationale for each choice.

**Step 4 — Deep Dive (15 min):**
Go 3 layers deep on 2–3 of the hardest components. Don't mention 10 things shallowly.

**Step 5 — Bottlenecks & Scale:**
- Where does this design break first?
- How do you address each bottleneck?

**Step 6 — Trade-off Summary:**
What was decided, what was traded off, and why.

### 10.1 URL Shortener

**The interesting parts** (not "store URL in DB, look it up"):
- ID generation: base-62 encoding of a numeric ID. Sequential IDs are predictable — use a distributed ID generator (Snowflake) or random + collision detection.
- Redirect latency < 10ms requirement → pure cache lookup, no DB on the hot path.
- Analytics: don't count clicks synchronously in the redirect path. Write click events to a queue (Kafka), process asynchronously. The redirect should be fire-and-forget.

### 10.4 Social Feed / Timeline

See [Fan-out on Write vs Fan-out on Read](#68-fan-out-on-write-vs-fan-out-on-read) above.

**Additional components:**
- Redis sorted set for timeline storage: `ZRANGEBYSCORE timeline:user_id -inf +inf LIMIT 0 20`
- Fanout service as a separate async process (not in the write path)
- Media storage: separate from tweet metadata (S3 for images/video, CDN for delivery)

### 10.5 Chat System (WhatsApp Model)

**The hard problems:**
1. **Message delivery guarantees:** At-least-once at the protocol level, with client-side deduplication by message ID.
2. **Online presence:** Heartbeats every 30 seconds. Presence service with TTL-based state. Don't compute presence on every read — cache it.
3. **Message ordering:** Monotonically increasing sequence numbers per chat. The server assigns the sequence number — not the client.
4. **Connection handling:** WebSocket per client. At 1M concurrent users, 1M open connections. Use connection servers separate from business logic servers.

### 10.9 Ride-Sharing (Uber Model)

**The core infrastructure challenge:** matching riders to drivers in real-time.

- **Location updates:** Drivers send GPS updates every 4 seconds via WebSocket. High write throughput, short retention — use a time-series DB or Redis with TTL.
- **Geospatial indexing:** Quadtree or geohash for efficient "find drivers within X km" queries. PostGIS (PostgreSQL extension) works at moderate scale; custom geospatial index at Uber's scale.
- **Matching:** Separate service. Inputs: rider location, driver locations. Output: best driver. Optimization problem — minimize ETA, not just distance.
- **Supply/demand:** Surge pricing is a signal to drivers, not just a revenue mechanism. The matching engine and pricing engine are separate concerns.

---

## Numbers Every Engineer Must Know

These are orders-of-magnitude estimates. Use them to reason about design, not to spec hardware.

### Latency Hierarchy

| Operation | Latency | Notes |
|---|---|---|
| L1 cache reference | 0.5 ns | |
| L2 cache reference | 3 ns | 6x L1 |
| Branch mispredict | 5 ns | |
| Mutex lock/unlock | 15 ns | Uncontended |
| Main memory (RAM) | 50–100 ns | 100–200x L1 |
| SSD random read (4KB) | 20,000 ns (20 µs) | |
| Read 1MB from SSD | 1,000,000 ns (1 ms) | |
| Same datacenter roundtrip | 500,000 ns (0.5 ms) | |
| HDD seek | 5,000,000 ns (5 ms) | 10x SSD random read |
| Read 1MB from HDD | 10,000,000 ns (10 ms) | |
| Cross-region (CA → EU) | 100–150 ms | |
| S3 PUT | 10–100 ms | Highly variable |

**The number to internalize:** RAM is 100,000x faster than disk. Network is 10,000x faster than disk. An extra network hop is expensive. An extra disk seek is catastrophic.

### Throughput Benchmarks

| System | Throughput |
|---|---|
| Single web server | 1K–10K req/s |
| PostgreSQL (simple queries) | 10K–50K queries/s |
| Redis | 100K+ ops/s |
| RabbitMQ (with acks) | 50K–100K msg/s |
| Kafka (3-node cluster, tuned) | 2M+ msg/s |

### Scale Milestones

| Users | Architecture Typical Pain Point |
|---|---|
| 1K | Single server, no scaling needed. Database is the likely bottleneck. |
| 10K | Add read replica. Consider caching layer. |
| 100K | Database sharding or move writes to queue. CDN for static assets. |
| 1M | Full horizontal scaling. Cache everything. Async processing. |
| 10M | Multiple datacenters. Database per service. Dedicated teams per service. |
| 100M+ | Custom infrastructure. Platform engineering teams. |

### Real-World Scale Numbers

| System | Scale |
|---|---|
| Twitter peak write fanout (Super Bowl) | ~150K writes/sec |
| YouTube uploads | ~500 hours of video per minute |
| WhatsApp at Facebook acquisition (2014) | 450M users, 50 engineers |
| Instagram at Facebook acquisition (2012) | 30M users, 13 engineers |
| Discord messages stored | 4 trillion+ (as of 2023) |
| Stripe queries processed | 5M+ queries/second |
| Stripe payment volume | $1.4 trillion in 2024 |

---

## Technology Comparisons

### SQL vs NoSQL Decision Matrix

| Criterion | PostgreSQL | MongoDB | Cassandra | DynamoDB | Redis |
|---|---|---|---|---|---|
| ACID transactions | Full | Single-doc | None native | Limited | None (single-op atomic) |
| Query flexibility | High (SQL) | Medium (query DSL) | Low (by partition key) | Low | None (key only) |
| Horizontal scale | Hard | Medium | Designed for it | Managed | Cluster mode |
| Write throughput | 10K–50K/s | 10K–50K/s | 100K+/s | Unlimited (managed) | 100K+/s |
| Strong consistency | Yes | Yes | Tunable | Tunable | Yes (single node) |
| Best for | Relational data, reporting | Flexible schemas, documents | High write throughput, time-series | AWS-native, serverless | Caching, sessions, pub-sub |

### Redis vs Memcached

| Dimension | Redis | Memcached |
|---|---|---|
| Data structures | Strings, Lists, Sets, Sorted Sets, Hashes, Streams, Geospatial | Strings only |
| Persistence | RDB + AOF (configurable) | None |
| Replication | Master-replica + Redis Cluster | None |
| Pub/Sub | Yes | No |
| Multi-threading | Single-threaded command execution | Multi-threaded |
| Memory efficiency | Slightly lower | Slightly higher (pure strings) |

**Verdict:** Redis wins almost every comparison today. Choose Redis by default.

### Kafka vs RabbitMQ vs SQS

| Dimension | Kafka | RabbitMQ | Amazon SQS |
|---|---|---|---|
| Latency (p99) | 5–15ms (batched) | <1ms | 20–50ms |
| Throughput | 2M+ msg/s (cluster) | 50K–100K msg/s | Unlimited (managed) |
| Message replay | Yes (core feature) | Streams only (v3.9+) | No |
| Ordering | Per-partition | Per-queue | FIFO queues only |
| Message priority | No | Yes (255 levels) | No |
| Exactly-once delivery | Yes (with transactions) | Yes | No (FIFO: yes) |
| Operational overhead | High | Medium | Zero |
| Monthly cost (medium scale) | $1,650+ (Confluent Cloud) | $816 (Amazon MQ) | $3K–$31K (pay per message) |

**Decision:**
- **Kafka:** Event replay, >100K msg/s, stream processing, event sourcing
- **RabbitMQ:** Complex routing, sub-ms latency, message priorities, IoT (MQTT)
- **SQS:** AWS-native, zero ops, simple background job queues

### CDN Comparison

| Dimension | Cloudflare | AWS CloudFront | Akamai |
|---|---|---|---|
| Edge nodes | 300+ cities, 125+ countries | 400+ PoPs | 4,100+ nodes, 130+ countries |
| Average latency | <50ms major metros | 50–100ms globally | <30ms (largest footprint) |
| Edge compute | Workers (<5ms cold start) | Lambda@Edge (10–30ms) | Rule engine (declarative) |
| DDoS protection | Built-in, automatic | AWS Shield (separate tier) | Prolexic (enterprise) |
| Pricing | Free / $20 / $200 / Enterprise | $0.085–0.17/GB | Enterprise contract |
| Propagation speed | <30 seconds | ~2 minutes | 10–15 minutes |
| Lock-in | Low | High (AWS-native) | High |

**Decision:**
- **Cloudflare:** Default for startups and mid-size. Best DX, fastest propagation.
- **CloudFront:** AWS-native stack, tight S3/Lambda integration matters.
- **Akamai:** Enterprise video streaming at massive scale, regulatory requirements.

---

## Real-World Case Studies

These are the case studies worth studying. Each one illustrates a principle better than any abstract explanation.

### Discord — Database Migration at Scale (2023)
**Topic: NoSQL database selection, hot partitions, operational toil**

Discord migrated from Cassandra (177 nodes) to ScyllaDB (72 nodes) with 4 trillion messages:
- **Why leave Cassandra:** Java GC pauses causing unpredictable p99 latency spikes; hot partition cascading failures
- **Why ScyllaDB:** Written in C++ (no GC), shard-per-core architecture eliminates cross-shard contention
- **Results:** p99 read latency: 40–125ms → 15ms; p99 write latency: 5–70ms → 5ms
- **Rust data services:** Request coalescing — 1,000 concurrent requests for same channel_id → 1 database query
- **Migration:** 9 days, at 3.2M messages/second, zero downtime

Source: [discord.com/blog/how-discord-stores-trillions-of-messages](https://discord.com/blog/how-discord-stores-trillions-of-messages)

### Cloudflare — Cascading Failure from Third-Party Dependency (2025)
**Topic: Availability engineering, active-active architecture, failure isolation**

GCP outage in June 2025 cascaded through Cloudflare Workers KV, taking down static asset delivery:
- **Root cause:** Two third-party object storage providers in active-active config, but reads were routed to only one provider per geography → inconsistencies persisted indefinitely
- **New architecture:** Small objects (median: 288 bytes) → Cloudflare's own distributed DB with 3-way replication; large objects → R2
- **Result:** p99 internal latency: ~200ms → <5ms; eliminated external dependency in the critical path

Source: [blog.cloudflare.com/rearchitecting-workers-kv-for-redundancy](https://blog.cloudflare.com/rearchitecting-workers-kv-for-redundancy/)

### Stripe — 5.5 Nines at Scale (2024)
**Topic: Zero-downtime data migrations, reliability at financial scale**

Stripe processes $1.4 trillion in payments annually at 5M+ queries/second:
- **DocDB:** Internal document database layer on top of MongoDB Community — abstraction enabling migrations without downtime
- **Data Movement Platform:** Live migrations via dual-writing, gradual traffic shifting, automated verification
- **Deploy cadence:** 16.4 deployments/day in 2022; 1,100 automatically rolled back
- **Reliability:** 5.5 nines (99.999% uptime)

Source: [stripe.com/blog/engineering](https://stripe.com/blog/engineering)

### Uber — Domain-Oriented Microservices
**Topic: Microservice organization at extreme scale**

Uber's problem: thousands of microservices with no organizing principle → ownership confusion, unpredictable blast radius.

DOMA framework — 5 layers:
1. Infrastructure (logging, storage, compute)
2. Business (trip, payment, driver)
3. Product (UberX, UberEats)
4. Presentation (mobile apps, web)
5. Edge (API gateway, auth)

Rule: services can only call down the stack (Product can call Business, not vice versa). Cross-layer calls are explicit contracts.

Source: [eng.uber.com/microservice-architecture/](https://eng.uber.com/microservice-architecture/)

### Netflix — Resilience at 65M Concurrent Viewers
**Topic: Chaos engineering, cell-based architecture**

Netflix runs Chaos Monkey in production — randomly killing production instances to ensure the system handles failures automatically. Cell-based architecture ensures that a live streaming failure (e.g., a boxing match) doesn't cascade to affect on-demand viewing.

Source: [netflixtechblog.com](https://netflixtechblog.com/)

### Meta — Scaling Threads to 100M Users in 5 Days (2023)
**Topic: Leveraging existing infrastructure, infrastructure re-use**

Meta launched Threads in July 2023, reaching 100M users in 5 days — the fastest app growth in history. Key: they built on top of Instagram's existing infrastructure (same data centers, same CDN, same ad infrastructure, same feed ranking). The lesson: greenfield infrastructure at scale is a multi-year project. Platform leverage is the only way to move fast at the scale Meta operates at.

Source: [engineering.fb.com](https://engineering.fb.com/)

---

## Interview Preparation

### What Interviewers Actually Evaluate

Based on FAANG interview data, approximate scoring weights:

| Dimension | Weight | What It Means |
|---|---|---|
| Judgment | 32% | Clarifying questions, stated assumptions, commitment to decisions |
| Technical Depth | 30% | 2–3 components understood deeply, not 10 mentioned shallowly |
| Operational Maturity | 20% | Monitoring, deployment, rollback, cost reasoning, failure modes |
| Communication | 18% | Handling pushback, incorporating feedback |

### Level Expectations

**L4 (Mid-level):** Draws correct architecture, explains components, makes reasonable choices. Shows capacity estimation.

**L5 (Senior):** Proactively identifies the *hardest part* of the system. Goes 3 layers deep on 2–3 components unprompted. Discusses failure modes and names specific technologies with reasoning.

**L6 (Staff):** Drives the conversation. Addresses operational concerns without prompting (monitoring, deployment, cost at scale). Reasons about multi-region evolution unprompted.

### The 5 Mistakes That Kill Otherwise Good Answers

1. **Jumping to solutions** before clarifying requirements (most common L4 failure)
2. **Over-engineering** for hypothetical scale not established in requirements
3. **Hedging everything** — "it depends" without committing to a choice
4. **Breadth over depth** — 10 components mentioned shallowly instead of 3 explained deeply
5. **Skipping operational concerns** — no monitoring, failure scenarios, or rollback plan

### 45-Minute Interview Time Budget

| Phase | Time | Goal |
|---|---|---|
| Clarify and scope | 5–10 min | Ask 3–5 targeted questions that visibly narrow the problem |
| Data model and API | 5–10 min | Define stored data; sketch API with request/response shapes |
| High-level architecture | 15–20 min | 5–7 boxes with narrated rationale for each choice |
| Deep dive + stress test | 15–20 min | 3 layers deep on 2–3 components; walk through failure modes |

---

## External Resources

### Official Engineering Blogs (Primary Sources)

| Company | Blog URL | Best Topics |
|---|---|---|
| Netflix | [netflixtechblog.com](https://netflixtechblog.com/) | Resilience, chaos engineering, streaming |
| Uber | [eng.uber.com](https://eng.uber.com/) | Microservices, geospatial, real-time |
| Discord | [discord.com/blog](https://discord.com/blog/engineering) | Database at scale, Rust, WebSockets |
| Cloudflare | [blog.cloudflare.com](https://blog.cloudflare.com/) | CDN, DDoS, edge computing, availability |
| Stripe | [stripe.com/blog/engineering](https://stripe.com/blog/engineering) | Financial systems, reliability, migrations |
| Meta | [engineering.fb.com](https://engineering.fb.com/) | Scale, feed ranking, infrastructure |
| Slack | [slack.engineering](https://slack.engineering/) | Messaging, reliability, migrations |
| LinkedIn | [engineering.linkedin.com/blog](https://engineering.linkedin.com/blog) | Kafka (invented here), data infrastructure |
| GitHub | [github.blog/engineering](https://github.blog/category/engineering/) | Git at scale, deployment, reliability |

### Curated Collections

- [github.com/ashishps1/awesome-engineering-articles](https://github.com/ashishps1/awesome-engineering-articles) — 300+ categorized engineering blog posts
- [roadmap.sh/system-design](https://roadmap.sh/system-design) — Visual interactive roadmap
- [github.com/donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer) — The canonical open-source reference

### Books

| Book | What It's Best For |
|---|---|
| *Designing Data-Intensive Applications* (Kleppmann) | The definitive reference on databases, replication, consistency |
| *Site Reliability Engineering* (Google) | SLOs, error budgets, operational practices |
| *Building Microservices* (Newman) | Service decomposition, service mesh, organizational patterns |
| *The Art of Scalability* (Abbott & Fisher) | Scale cube, organizational scaling |

### Latency Reference

- [gist.github.com/jboner/2841832](https://gist.github.com/jboner/2841832) — Jeff Dean's original "Latency Numbers Every Programmer Should Know"
- [colin-scott.github.io/personal_website/research/interactive_latency.html](https://colin-scott.github.io/personal_website/research/interactive_latency.html) — Interactive latency chart across years

---

*Maintained by Nitish Kushwaha. Last updated: June 2026.*
*To contribute: open a PR with a topic, case study, or correction. Include sources.*
