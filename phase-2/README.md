# Phase 2 — Networking & Communication

Networking is the connective tissue of distributed systems. Every component in your architecture communicates over a network, and network behavior determines latency, reliability, and failure modes.

## Why This Phase Matters
You cannot design a distributed system without understanding how data moves between machines — protocols, proxies, load balancers, and real-time transports are the building blocks of every architecture.

## Learning Path
**Timeline:** 2 weeks (~14-16 hours)
**Recommended pace:** 1 section per 2-3 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 2.1 | [TCP vs UDP — When Each Matters](./2.1-tcp-vs-udp.md) | Reliability, ordering, handshake, QUIC, use-case decision | 2h |
| 2.2 | [HTTP/1.1 vs HTTP/2 vs HTTP/3](./2.2-http-versions.md) | Multiplexing, HOL blocking, QUIC, TLS, adoption | 2-3h |
| 2.3 | [DNS and How It Affects Architecture](./2.3-dns.md) | Resolution, TTL, GeoDNS, anycast, failover, outages | 2h |
| 2.4 | [Load Balancers (L4 vs L7)](./2.4-load-balancers.md) | Layer 4 vs 7, algorithms, health checks, sticky sessions | 2-3h |
| 2.5 | [Reverse Proxies](./2.5-reverse-proxies.md) | TLS termination, caching, rate limiting, nginx vs Envoy | 2h |
| 2.6 | [CDNs — How They Work and When to Use Them](./2.6-cdns.md) | Edge caching, cache-control, origin pull, provider comparison | 2-3h |
| 2.7 | [Long Polling, SSE, and WebSockets](./2.7-realtime-communication.md) | Real-time patterns, trade-offs, connection scaling, Discord | 2h |

## Prerequisites
- Phase 1 complete (especially 1.3 Latency vs Throughput and 1.5 Stateless vs Stateful)
- Basic networking: what IP addresses, ports, and HTTP requests are
- Familiarity with what a web server does

## Phase Goals

By the end of Phase 2, you should be able to:

1. Choose TCP vs UDP for a given use case and explain the exact reason
2. Explain the head-of-line blocking problem and how HTTP/2 and HTTP/3 address it differently
3. Describe the full DNS resolution chain and how TTL affects your deployment strategy
4. Distinguish L4 from L7 load balancing and pick the right algorithm for a scenario
5. Explain what a reverse proxy does that a load balancer does not
6. Describe how a CDN cache hit/miss works and write correct Cache-Control headers
7. Compare WebSockets, SSE, and long polling — and pick the right one for a given real-time feature

## Navigation

| | |
|---|---|
| ⬅️ Phase 1 | [Foundations of Distributed Systems](../phase-1/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 3 | [Data Storage at Scale](../phase-3/README.md) |
