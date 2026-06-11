# Phase 6 — Scalability Patterns

Knowing how to build a system is not the same as knowing how to build one that survives growth. Phase 6 covers the patterns that separate systems which scale gracefully from those that require full rewrites at 10x load.

## Why This Phase Matters

Scalability patterns are the difference between a system that degrades under load and one that holds. These are not theoretical — rate limiting, circuit breakers, idempotency, and the saga pattern appear in every major production system at scale.

## Learning Path

**Timeline:** 2 weeks (~16-18 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 6.1 | [The 12-Factor App](./6.1-twelve-factor-app.md) | Config, statelessness, process model, cloud-native design | 2h |
| 6.2 | [Rate Limiting](./6.2-rate-limiting.md) | Token bucket, leaky bucket, sliding window, Redis implementation | 2-3h |
| 6.3 | [Circuit Breakers & Bulkheads](./6.3-circuit-breakers-bulkheads.md) | States, failure isolation, thread pools, Resilience4j | 2h |
| 6.4 | [Retry Strategies with Exponential Backoff](./6.4-retry-exponential-backoff.md) | Jitter, retry storms, idempotency requirement, AWS SDK | 2h |
| 6.5 | [Idempotency](./6.5-idempotency.md) | Idempotency keys, deduplication, payment processing, at-least-once | 2h |
| 6.6 | [Saga Pattern for Distributed Transactions](./6.6-saga-pattern.md) | Choreography vs orchestration, compensating transactions | 2-3h |
| 6.7 | [CQRS & Event Sourcing](./6.7-cqrs-event-sourcing.md) | Command/query separation, event store, projections, trade-offs | 2-3h |
| 6.8 | [Fan-out on Write vs Fan-out on Read](./6.8-fan-out-write-vs-read.md) | Push vs pull, write amplification, celebrity problem, hybrid | 2h |

## Prerequisites

- Phases 1-5 complete
- Phase 5 especially (messaging is the backbone of saga, CQRS, and fan-out patterns)

## Phase Goals

By end of Phase 6 you should be able to:

1. Apply the 12-factor methodology to a new service design
2. Implement a rate limiter using token bucket or sliding window and choose between them
3. Design a circuit breaker and explain all three states with transition conditions
4. Write retry logic with exponential backoff + jitter and explain why jitter matters
5. Implement idempotency keys for a payment or order processing flow
6. Choose between saga choreography and orchestration and design compensating transactions
7. Explain CQRS and event sourcing trade-offs, and when they are over-engineering
8. Design a timeline/feed system using the right fan-out strategy for a given scale

## Navigation

| | |
|---|---|
| ⬅️ Phase 5 | [Messaging & Async Processing](../phase-5/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 7 | [Microservices & Service Architecture](../phase-7/README.md) |
