# Phase 10 — Classic System Design Problems

Opening: this is the capstone phase. Every problem is a real FAANG interview question. Each walkthrough follows the same format a principal engineer uses in a real design review.

## How to Use This Phase
1. Read the requirements and close the document
2. Spend 30-45 minutes designing it yourself on paper
3. Compare your design to the walkthrough
4. Identify specifically what you missed and why
5. Redo the design incorporating what you learned

Reading without designing is how engineers stay stuck at mid-level.

## Problems in This Phase

| # | Problem | Key Challenge | Est. Time |
|---|---|---|---|
| 10.1 | [Design a URL Shortener](./10.1-url-shortener.md) | ID generation, < 10ms redirect, async analytics | 3h |
| 10.2 | [Design a Rate Limiter](./10.2-rate-limiter.md) | Distributed counting, race conditions, window accuracy | 3h |
| 10.3 | [Design a Notification System](./10.3-notification-system.md) | Multi-channel, fan-out at scale, delivery guarantees | 3h |
| 10.4 | [Design a Social Feed / Timeline](./10.4-social-feed-timeline.md) | Fan-out hybrid model, celebrity problem, ranking | 4h |
| 10.5 | [Design a Chat System](./10.5-chat-system.md) | Message ordering, delivery receipts, WebSocket scale | 4h |
| 10.6 | [Design a Search Autocomplete](./10.6-search-autocomplete.md) | Trie vs index, top-K, sub-100ms latency | 3h |
| 10.7 | [Design a Distributed Cache](./10.7-distributed-cache.md) | Consistent hashing, stampede, eviction, HA | 3h |
| 10.8 | [Design a File Storage System](./10.8-file-storage-system.md) | Chunked upload, deduplication, sync, conflicts | 4h |
| 10.9 | [Design a Ride-Sharing Service](./10.9-ride-sharing-service.md) | Geospatial matching, real-time location, dispatch | 4h |
| 10.10 | [Design a Video Streaming Platform](./10.10-video-streaming-platform.md) | Transcoding pipeline, adaptive bitrate, CDN | 4h |

## Recommended Order
Start with 10.1, 10.2 (simpler scope, good warm-ups). Then 10.5, 10.4 (core interview problems). 10.9 and 10.10 are the hardest — do them last.

## What Separates Good from Great
**Good (L5 pass):** Correct architecture, reasonable choices, handles the happy path.
**Great (L6 hire):** Proactively identifies the hardest part. Goes 3 layers deep on 2 components. Brings up operational concerns without prompting. Has actual numbers memorized.

## Navigation

| | |
|---|---|
| ⬅️ Phase 9 | [Security at Scale](../phase-9/README.md) |
| 🏠 Curriculum | [Main README](../README.md) |
