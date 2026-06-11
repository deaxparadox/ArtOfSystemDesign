# Phase 7 — Microservices & Service Architecture

Microservices are the dominant architectural pattern at scale — but they are also the most over-applied. This phase covers not just how microservices work, but when they make sense and when a well-structured monolith is the better engineering decision.

## Why This Phase Matters

Most engineers have worked in a microservices environment without understanding why the boundaries were drawn where they were. This phase gives you the mental models to make those decisions deliberately — and to recognize when your system is paying the microservices tax without getting the benefits.

## Learning Path

**Timeline:** 2 weeks (~14-16 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 7.1 | [Monolith vs Microservices](./7.1-monolith-vs-microservices.md) | Honest trade-offs, when each wins, migration patterns | 2-3h |
| 7.2 | [Service Discovery](./7.2-service-discovery.md) | Client-side vs server-side, Consul, Kubernetes DNS, health checks | 2h |
| 7.3 | [API Gateways](./7.3-api-gateways.md) | Routing, auth, rate limiting, BFF pattern, Kong vs AWS APIGW | 2h |
| 7.4 | [Service Meshes](./7.4-service-meshes.md) | Sidecar proxy, mTLS, observability, Istio vs Linkerd, overhead | 2-3h |
| 7.5 | [Inter-Service Communication](./7.5-inter-service-communication.md) | REST vs gRPC vs events, coupling, latency, when each fits | 2h |
| 7.6 | [Distributed Tracing](./7.6-distributed-tracing.md) | Spans, context propagation, sampling, OpenTelemetry, Jaeger | 2h |
| 7.7 | [When to Use a Monolith](./7.7-when-to-use-monolith.md) | Modular monolith, the microservices regret pattern, decision framework | 2h |

## Prerequisites

- Phases 1-6 complete
- Phase 2 especially (networking fundamentals underpin all service communication)
- Phase 6 (circuit breakers, retries, and sagas are microservices-native patterns)

## Phase Goals

By end of Phase 7 you should be able to:

1. Make a justified monolith vs microservices decision for a given team size and product stage
2. Design a service discovery mechanism and explain client-side vs server-side approaches
3. Design an API gateway with auth, rate limiting, and routing — and know when to use a BFF
4. Explain what a service mesh provides that a load balancer does not
5. Choose between REST, gRPC, and event-driven communication for a given inter-service interaction
6. Instrument a distributed trace and explain sampling strategy trade-offs
7. Argue for a monolith over microservices in an interview with specific numbers and reasoning

## Navigation

| | |
|---|---|
| ⬅️ Phase 6 | [Scalability Patterns](../phase-6/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 8 | [Reliability & Operations](../phase-8/README.md) |
