# Phase 5 — Messaging & Async Processing

Synchronous request-response works fine at small scale. At 10M events/day, it becomes a liability — one slow downstream service can cascade failures across your entire system. Async messaging decouples producers from consumers, absorbs traffic spikes, and enables the kind of independent scaling that makes large systems survivable.

## Why This Phase Matters
Every major distributed system at scale uses async messaging somewhere. Kafka powers LinkedIn, Uber, Netflix, and thousands of others. Understanding when and how to use async processing is the difference between a system that degrades gracefully and one that falls over when load spikes.

## Learning Path
**Timeline:** 2 weeks (~14-16 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 5.1 | [Why Async? The Producer-Consumer Model](./5.1-why-async-producer-consumer.md) | Decoupling, async benefits, when sync fails, use cases | 2h |
| 5.2 | [Message Queues vs Event Streams](./5.2-message-queues-vs-event-streams.md) | Queue vs log, replay, retention, ordering, fan-out | 2h |
| 5.3 | [Kafka Architecture & Guarantees](./5.3-kafka-architecture.md) | Partitions, offsets, ISR, consumer groups, exactly-once | 3h |
| 5.4 | [RabbitMQ vs Kafka vs SQS](./5.4-rabbitmq-vs-kafka-vs-sqs.md) | Latency, throughput, routing, replay, cost, operations | 2h |
| 5.5 | [At-Least-Once vs Exactly-Once Delivery](./5.5-delivery-guarantees.md) | Delivery semantics, idempotency, deduplication, trade-offs | 2h |
| 5.6 | [Dead Letter Queues](./5.6-dead-letter-queues.md) | Poison messages, retry strategies, DLQ monitoring | 2h |
| 5.7 | [Backpressure & Flow Control](./5.7-backpressure-flow-control.md) | Consumer lag, reactive streams, overload protection | 2h |

## Prerequisites
- Phase 1 complete (especially 1.4 Horizontal vs Vertical Scaling)
- Phase 3 complete (especially 3.1 Relational vs NoSQL)
- Phase 4 complete (caching patterns are closely related to async processing)

## Phase Goals

By the end of Phase 5, you should be able to:

1. Explain why async decoupling improves resilience and give a concrete failure scenario where sync would have cascaded
2. Distinguish message queues from event streams and pick the right one for a given use case
3. Explain Kafka partitions, offsets, and consumer groups — and size a Kafka cluster for a given throughput
4. Choose between RabbitMQ, Kafka, and SQS with a concrete reason for a given scenario
5. Explain exactly-once delivery semantics and why idempotent consumers are usually the pragmatic choice
6. Design a DLQ strategy including retry policy, monitoring, and replay mechanism
7. Detect and handle backpressure before it causes an outage

## Navigation

| | |
|---|---|
| ⬅️ Phase 4 | [Caching](../phase-4/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 6 | [Scalability Patterns](../phase-6/README.md) |
