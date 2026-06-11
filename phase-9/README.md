# Phase 9 — Security at Scale

Security is not a feature you add at the end — it is a property of the architecture. At scale, the attack surface grows with every new service, endpoint, and engineer. This phase covers the security patterns that production systems at Google, Cloudflare, Stripe, and GitHub actually use.

## Why This Phase Matters

A single misconfigured JWT validation, an unrotated secret, or a missing rate limit has caused billion-dollar breaches. Security at scale is not about paranoia — it is about knowing which controls matter, at which scale, and implementing them correctly the first time.

## Learning Path

**Timeline:** 1.5 weeks (~10-12 hours)
**Recommended pace:** 1 section per 2 days

## Topics in This Phase

| # | Topic | Key Concepts | Est. Time |
|---|---|---|---|
| 9.1 | [Authentication at Scale — OAuth2, OIDC, JWT](./9.1-authentication-oauth2-oidc-jwt.md) | Auth flows, token validation, refresh, session management | 2-3h |
| 9.2 | [Zero-Trust Architecture](./9.2-zero-trust-architecture.md) | Never trust always verify, BeyondCorp, ZTNA, identity perimeter | 2h |
| 9.3 | [API Security](./9.3-api-security.md) | OWASP API Top 10, rate limiting, input validation, secrets mgmt | 2h |
| 9.4 | [DDoS Mitigation Patterns](./9.4-ddos-mitigation.md) | Attack types, anycast, scrubbing, Cloudflare, AWS Shield | 2h |
| 9.5 | [mTLS in Service Meshes](./9.5-mtls-service-meshes.md) | Mutual TLS, certificate rotation, Istio, service identity | 2h |

## Prerequisites

- Phases 1-8 complete
- Phase 2 (TLS, HTTP) and Phase 7 (service meshes) especially relevant
- Basic understanding of public key cryptography (what a certificate is)

## Phase Goals

By end of Phase 9 you should be able to:

1. Implement OAuth2 authorization code flow with PKCE and explain why each step exists
2. Explain zero-trust principles and how they differ from perimeter security
3. Identify the OWASP API Top 10 risks and name a mitigation for each
4. Design a DDoS mitigation strategy distinguishing L3/L4 from L7 attacks
5. Explain mTLS — what it proves, how certificates are rotated, and why a service mesh helps

## Navigation

| | |
|---|---|
| ⬅️ Phase 8 | [Reliability & Operations](../phase-8/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
| ➡️ Phase 10 | [Classic System Design Problems](../phase-10/README.md) |
