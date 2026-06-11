# Phase 1 — Foundations of Distributed Systems

Phase 1 establishes the mental model that every subsequent phase builds on. Before you can design systems that handle millions of requests, survive data center failures, or stay consistent across continents, you need to understand what distribution actually does to a system — and why it is fundamentally harder than running software on a single machine. This phase covers the vocabulary, the failure modes, and the engineering trade-offs that define every decision you will make in Phases 2 through 10.

## Why Start Here?

All of Phases 2-10 are solutions to problems created by distribution. Without understanding the problems, the solutions feel like trivia.

Caching exists because latency is real and unpredictable. Load balancers exist because a single machine has a ceiling. Consensus algorithms exist because you cannot trust a message to arrive. Service meshes exist because the network is not reliable. If you skip Phase 1 and jump straight to "how does Kafka work," you will memorize the answer but you will not understand when to reach for it — or when not to. Every advanced concept in system design is a response to a constraint introduced the moment you put a second machine in the picture.

## Learning Path
**Timeline:** 2 weeks (~12-15 hours)
**Recommended pace:** 1 section per 2-3 days with practice problems

## Topics in This Phase

| # | Topic | Key Concepts Covered | Est. Time |
|---|---|---|---|
| 1.1 | [What Is a Distributed System?](./1.1-what-is-a-distributed-system.md) | Partial failure, consensus, properties, why distribution is hard | 2-3h |
| 1.2 | [The 8 Fallacies of Distributed Computing](./1.2-eight-fallacies.md) | Network assumptions, what breaks in production, real outages | 2h |
| 1.3 | [Latency vs Throughput](./1.3-latency-vs-throughput.md) | p50/p99/p999, tail latency, Little's Law, optimization trade-offs | 2-3h |
| 1.4 | [Horizontal vs Vertical Scaling](./1.4-horizontal-vs-vertical-scaling.md) | Scale-up vs scale-out, when each fails, decision framework | 2h |
| 1.5 | [Stateless vs Stateful Systems](./1.5-stateless-vs-stateful.md) | Session management, JWT, sticky sessions, Kubernetes implications | 2h |
| 1.6 | [SLAs, SLOs, SLIs — What They Actually Mean](./1.6-slas-slos-slis.md) | Error budgets, reliability math, Google SRE approach | 2h |

## Prerequisites

This is Phase 1 — no distributed systems prerequisites.

Basic comfort needed:
- Programming in any language (examples use Python but concepts are language-agnostic)
- What a web server is: receives HTTP requests, returns responses
- Basic networking: IP addresses, ports, what a request/response cycle is

## Phase Goals

By the end of Phase 1, you should be able to:

1. **Explain what makes a system "distributed"** and list 3+ failure modes that only exist in distributed systems
2. **Recall all 8 fallacies** and give a real production example for each one
3. **Define latency vs throughput**, explain the trade-off, and give numbers for p99 expectations at scale
4. **Decide whether to scale horizontally or vertically** given a specific scenario with a clear reason
5. **Explain stateless vs stateful** systems and why the distinction determines your scaling strategy
6. **Define SLI, SLO, and SLA** and explain error budgets to a non-technical stakeholder in 2 minutes

## How to Study Each Section

1. Read the theory section without taking notes
2. Draw the ASCII diagram from memory
3. Explain the concept out loud as if in an interview
4. Check the "Interview Perspective" section to see where you missed depth
5. Move to the next section

## Navigation

| | |
|---|---|
| ⬅️ Curriculum | [Main README](../README.md) |
| ➡️ Phase 2 | [Networking & Communication](../phase-2/README.md) |
