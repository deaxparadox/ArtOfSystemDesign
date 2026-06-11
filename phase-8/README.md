# Phase 8 — Reliability & Operations

Building a system that works is table stakes. Building one that stays working under failure, load spikes, and human error — that is engineering. Phase 8 covers the operational practices and architectural patterns that separate systems with 99.9% uptime from those with 99.99%.

## Why This Phase Matters

The difference between 99.9% and 99.99% availability is 8.7 hours of downtime per year vs 52 minutes. For a payment processor or a social platform, that gap is the difference between staying in business and losing customers to competitors. The practices in this phase are what Google SRE, Netflix, and Stripe actually run in production.

## Learning Path

**Timeline:** 2 weeks (~14-16 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 8.1 | [Fault Tolerance — What It Actually Means](./8.1-fault-tolerance.md) | Partial failure, isolation, redundancy, failure domains | 2h |
| 8.2 | [Replication & Redundancy](./8.2-replication-redundancy.md) | Active-active, active-passive, multi-region, AZ redundancy | 2h |
| 8.3 | [Chaos Engineering](./8.3-chaos-engineering.md) | Chaos Monkey, GameDays, fault injection, production testing | 2h |
| 8.4 | [Health Checks & Probes](./8.4-health-checks-probes.md) | Readiness vs liveness vs startup, Kubernetes probes, load balancer integration | 2h |
| 8.5 | [Graceful Degradation](./8.5-graceful-degradation.md) | Feature flags, fallbacks, partial functionality, user experience | 2h |
| 8.6 | [Disaster Recovery: RPO vs RTO](./8.6-disaster-recovery-rpo-rto.md) | Recovery objectives, backup strategies, failover, DR tiers | 2-3h |
| 8.7 | [Incident Management & Post-Mortems](./8.7-incident-management-postmortems.md) | Blameless culture, runbooks, on-call, root cause analysis | 2h |

## Prerequisites

- Phases 1-7 complete
- Phase 3 (replication) and Phase 6 (circuit breakers) especially relevant
- Familiarity with what SLOs and error budgets are (covered in Phase 1.6)

## Phase Goals

By end of Phase 8 you should be able to:

1. Define fault tolerance precisely and distinguish it from high availability and reliability
2. Design a redundancy strategy specifying active-active vs active-passive and justify the choice
3. Design a chaos engineering program — what to test, how to safely run experiments in production
4. Configure Kubernetes readiness vs liveness probes correctly and explain the difference
5. Design graceful degradation for a given feature — what degrades, what stays up, how users are informed
6. Define RPO and RTO for each tier of a system and map them to backup/replication strategies
7. Write a blameless post-mortem and explain why the "5 whys" matters for root cause analysis

## Navigation

| | |
|---|---|
| ⬅️ Phase 7 | [Microservices & Service Architecture](../phase-7/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 9 | [Security at Scale](../phase-9/README.md) |
