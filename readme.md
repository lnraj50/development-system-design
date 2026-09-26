The 30-Topic Practical System Design Blueprint
Author: Nagarajan Laxmanan Company: Marmato digital LLC, USA License: MIT Topics: 30 System Design Concepts Offline Ready

A comprehensive, production-grounded system design reference created for working software engineers, architects, and interview candidates. Instead of abstract whiteboard diagrams, every topic is anchored in concrete production incidents, failure mechanics, senior-level remediations, collapsible interview Q&As, and hands-on code exercises.

📖 Key Highlights
Everyday Developer Scenarios: Real-life incidents including the iPhone 18 single-unit flash sale (concurrency & deadlocks), Chrome tab crash isolation (process boundaries), payment gateway webhook fan-out (non-blocking I/O), and tail-latency hedging.
The Failure Mechanics: Deep dives into what breaks at scale—kernel context switching thrashing, connection pool exhaustion, cascading retry storms, database locks, cache stampedes, and dirty reads.
Production-Grade Solutions: Concrete architectural patterns using Redis atomic primitives (DECRBY), PostgreSQL row-level locking (FOR UPDATE), distributed locks, circuit breakers, idempotency keys, and token-bucket rate limiters.
Interview & Practical Q&A: Rigorous questions with practical senior-level answers under every topic.
Hands-On Exercises & Code: Runnable code snippets and worked solutions across Python, Go, SQL, and Bash.
Standalone Offline HTML: Zero runtime dependencies, system-aware light/dark theme toggle with persistent storage, collapsible panels, and instant client-side search.
📑 Topic Index
Part 1: Computing Basics
Topic 01 – Processes vs Threads: Virtual memory isolation, Chrome renderer crash domains, and thread-shared heap risks.
Topic 02 – CPU Scheduling & Context Switching: Linux CFS quotas, Kubernetes CPU throttling (cfs_quota_us), and thread-pool right-sizing.
Topic 03 – Blocking vs Non-Blocking I/O: Kernel I/O multiplexing (epoll/kqueue), event loops, and webhook fan-out throughput.
Topic 04 – Concurrency vs Parallelism (Race Conditions & Deadlocks): The iPhone 18 flash sale, Redis atomic counters, and row-level lock ordering.
Topic 05 – Memory: Stack vs Heap: Cache locality, pointer dereferencing overhead, and high-frequency GC memory leaks.
Part 2: Application Structure
Topic 06 – Monoliths vs Modular Codebases: Single-process deployment ergonomics vs runtime blast-radius isolation.
Topic 07 – Services & Service Boundaries: Domain-Driven Design (DDD), aggregate roots, and preventing distributed monoliths.
Topic 08 – Synchronous vs Asynchronous Execution: Fast user-facing acknowledgments vs asynchronous eventual consistency.
Topic 09 – Background Jobs & Workers: Dead-letter queues (DLQ), backoff strategies, and Poison Pill message isolation.
Topic 10 – Stateful vs Stateless Services: Ephemeral horizontal autoscaling vs sticky sessions and distributed state stores.
Part 3: Networking Fundamentals
Topic 11 – Anatomy of an HTTP Request: DNS lookup stages, TLS 1.3 handshake negotiation, TCP connection reuse, and head-of-line blocking.
Topic 12 – TCP vs UDP: Guaranteed ordered packet streams vs low-latency real-time telemetry and WebRTC media.
Topic 13 – Latency Sources in Distributed Systems: Cross-datacenter optical propagation limits, serialization overhead, and tail-latency hedging.
Topic 14 – Timeouts, Retries & Cascading Failures: Exponential backoff, full jitter algorithms, and circuit-breaker trip states.
Topic 15 – Load Balancers vs Reverse Proxies: Layer 4 vs Layer 7 routing, SSL termination, and consistent hash ring distribution.
Part 4: APIs & Communication
Topic 16 – REST APIs in the Real World: Resource modeling, RFC 7807 problem details, and semantic status code conventions.
Topic 17 – RPC and gRPC Basics: Protocol Buffers serialization efficiency, HTTP/2 multiplexing, and strongly typed IDLs.
Topic 18 – Event-Driven Architectures: Decoupled producer/consumer models, outbox patterns, and event-carried state transfer.
Topic 19 – Message Queues vs Event Streams: Ephemeral point-to-point queues (RabbitMQ/SQS) vs append-only partitioned commit logs (Kafka).
Topic 20 – Idempotency & Request Safety: Client-generated idempotency tokens, atomic database uniqueness, and duplicate charge mitigation.
Part 5: Containers & Deployment
Topic 21 – Docker & Containerization: Linux namespaces, cgroups resource enforcement, and copy-on-write union filesystems.
Topic 22 – Containers vs Virtual Machines: Shared OS kernel lightweight density vs Type-1/Type-2 hypervisor hardware virtualization.
Topic 23 – Kubernetes & Container Orchestration: Declarative reconciliation loops, pod lifecycle probes, and horizontal pod autoscaling.
Part 6: Data & Discovery
Topic 24 – Relational (SQL) vs Non-Relational (NoSQL) Databases: ACID transactional guarantees vs horizontal document/key-value sharding trade-offs.
Topic 25 – Indexes & Query Performance: B-tree branch traversals, composite index column ordering, and eliminating sequential table scans.
Topic 26 – Authentication vs Authorization: Identity verification (OAuth 2.0 / OIDC / JWT) vs granular permission enforcement (RBAC / ABAC).
Topic 27 – How Modern Search Works: Inverted indexes, tokenization, BM25 scoring, and vector embeddings for semantic recall.
Topic 28 – Caching & Cache Invalidation: Cache-aside vs write-through patterns, TTL strategies, and combating the Thundering Herd.
Part 7: Scaling & Reliability
Topic 29 – Vertical vs Horizontal Scaling: Saturated bare-metal upgrades vs shared-nothing multi-node horizontal elasticity.
Topic 30 – Sharding & Database Partitioning: Shard key cardinality, range vs hash partitioning, and eliminating cross-shard joins.
🚀 Viewing the Handbook
Option 1: Standalone Offline HTML
The interactive edition is bundled into a single zero-dependency HTML file:

Clone or download the repository.
Open system-design-blueprint_v2.html in any web browser.
Features:
Light / Dark Mode: Toggle at the top of the sidebar or top bar (remembers preference via localStorage).
Real-Time Topic Search: Instant filtering across all 30 topics.
Collapsible Interview Q&A: Expand or collapse senior-level interview questions.
Code Copy: 1-click clipboard copy for code implementations.
Option 2: Local Development
To run or preview within a local Node.js environment:

git clone https://github.com/<your-username>/system-design-handbook.git
cd system-design-handbook
npm install
npm run dev
💡 Example: Concurrency & Flash-Sale Race Conditions
Here is an excerpt from Topic 4 illustrating how production teams handle high-concurrency inventory drops:

import redis

r = redis.Redis(host='localhost', port=6379, decode_responses=True)

def purchase_limited_item(user_id: str, product_id: str) -> bool:
    stock_key = f"inventory:{product_id}:stock"
    # Atomic decrement runs in a single-threaded Redis engine pipeline
    remaining = r.decrby(stock_key, 1)
    
    if remaining < 0:
        # Revert count if sale already depleted
        r.incrby(stock_key, 1)
        return False
        
    # Enqueue confirmed purchase order for async checkout
    r.lpush("orders:pending", f"{user_id}:{product_id}")
    return True
Author: Nagarajan Laxmanan
Organization: Marmato digital LLC, USA
Specialization: Enterprise System Architecture, Scalable Distributed Systems & Cloud Platforms
📄 License
This repository is distributed under the MIT License. See LICENSE for details.
