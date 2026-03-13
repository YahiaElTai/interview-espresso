# Cloud Design Patterns

> **27 questions** — 17 theory, 7 practical, 3 experience

- What makes patterns cloud-native: ephemeral compute, network partitions, elastic scaling — why these constraints drive pattern adoption
- When to introduce a pattern vs keeping things simple
- Circuit breaker: states (closed/open/half-open), threshold tuning, composing with retry and bulkhead
- Retry and timeout patterns: exponential backoff with jitter, thundering herd prevention, retryable vs terminal errors, cascading timeout propagation, timeout budgets across call chains
- Bulkhead: resource isolation, preventing one slow downstream from starving others
- Saga pattern: orchestrator vs choreography, compensating transactions, idempotency requirements, state machine implementation — when choreography becomes unmanageable
- Competing consumers and queue-based load leveling: absorbing traffic spikes, priority queues and starvation prevention
- Cache-aside pattern: failure modes, thundering herd, cache stampede prevention — cloud-scale caching pitfalls
- CQRS: separate read/write models, scaling mismatch, eventual consistency costs, materialized views as read-optimized projections
- Event sourcing: storing events vs state, audit trails, schema evolution, replay
- Transactional outbox: solving the dual-write problem, polling publisher vs CDC, guaranteeing at-least-once event delivery alongside database writes
- Gateway aggregation / BFF: collapsing multiple backend calls into one client response, cross-cutting concerns at the edge, single-point-of-failure risk
- Health endpoint monitoring: liveness vs readiness semantics, shallow vs deep checks, cascading failure from overly strict checks
- Throttling pattern: server-side rate limiting vs client-side backoff, protecting services from burst traffic, interaction with retry and circuit breaker
- Backpressure: consumer-to-producer flow control, queue depth as a signal, difference from throttling and rate limiting

---

## Foundational

<details>
<summary>1. What makes a design pattern specifically "cloud-native" — how do the constraints of ephemeral compute (instances disappearing mid-request), network partitions (calls failing unpredictably), and elastic scaling (replicas changing constantly) force you toward patterns that wouldn't be necessary on a single reliable server, and what fundamental assumption about infrastructure changes when you move to the cloud?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>2. When should you introduce a cloud design pattern vs keeping the implementation simple — what are the signals that a pattern is genuinely needed, what is the cost of premature pattern adoption, and how do you evaluate whether the complexity a pattern introduces is justified by the problem it solves?</summary>

<!-- Answer will be added later -->

</details>

## Conceptual Depth

<details>
<summary>3. How does the circuit breaker pattern work — what are the three states (closed, open, half-open) and the transitions between them, how do you tune thresholds (failure count, timeout duration, half-open trial count) for different downstream services, and why does a circuit breaker need to compose with retry and bulkhead rather than working in isolation?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>4. Why is naive retry dangerous in distributed systems — how does exponential backoff with jitter prevent the thundering herd problem, how do you distinguish retryable errors (network timeout, 503) from terminal errors (400, 404), and what happens to a system when every client retries aggressively at the same time after a brief outage?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. How do timeout budgets work across a call chain (Service A calls B, B calls C, C calls D) — why does each service need to propagate remaining budget to downstream calls instead of using independent timeouts, what happens when you don't propagate budgets (wasted work, resource exhaustion), and how do you implement cascading timeout propagation in practice?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. What problem does the bulkhead pattern solve — how does isolating resources (thread pools, connection pools, memory) per downstream dependency prevent one slow or failing service from starving all other calls, and what are the tradeoffs of strict bulkhead isolation (wasted capacity when a partition is idle)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. How does the saga pattern coordinate distributed transactions without a traditional two-phase commit — what is the difference between orchestrator-based and choreography-based sagas, why do compensating transactions need to be idempotent, and at what point does choreography become unmanageable and you need an orchestrator?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. How do you implement a saga as a state machine — what states and transitions does the machine track, how does persisting the state machine enable crash recovery, and what happens to in-flight compensations if the orchestrator restarts mid-saga?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>9. How do competing consumers and queue-based load leveling absorb traffic spikes — what happens without a queue when burst traffic hits your service directly, how do priority queues work without causing starvation of lower-priority messages, and what are the tradeoffs of queue-based architectures (added latency, at-least-once complexity)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>10. What are the failure modes of the cache-aside pattern at cloud scale — what causes a thundering herd (cache miss storm after expiry or eviction), how does a cache stampede differ from a thundering herd, and what prevention techniques (locking, probabilistic early expiration, stale-while-revalidate) address each problem without introducing new bottlenecks?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>11. Why does CQRS separate read and write models instead of using a single model for both — what scaling mismatch does this solve, what are the costs of eventual consistency between the write store and the read-optimized projections (materialized views), and when does CQRS add unjustified complexity vs when is it genuinely necessary?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. How does event sourcing differ from traditional state-based persistence — why is storing every state change as an immutable event valuable for audit trails and temporal queries, what challenges does schema evolution introduce when your event shapes change over time, and what are the practical costs of event replay (rebuilding state from thousands of events)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. What is the dual-write problem in event-driven systems and how does the transactional outbox pattern solve it — what is the difference between polling publisher and change data capture (CDC) as delivery mechanisms, what consistency guarantees does each approach provide, and why is at-least-once delivery the practical ceiling for outbox-based systems?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>14. How does the gateway aggregation (Backend-for-Frontend) pattern reduce client-server round trips by collapsing multiple backend calls into a single response — what cross-cutting concerns (authentication, rate limiting, response shaping) does the gateway handle, what is the single-point-of-failure risk it introduces, and when does a BFF become an anti-pattern that couples too many services together?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>15. Why does health endpoint monitoring need to distinguish between liveness and readiness — what does each check semantically mean, when should you use shallow checks (process alive, port open) vs deep checks (database reachable, downstream healthy), and how do overly strict health checks cause cascading failures where a transient downstream issue takes down your entire service fleet?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>16. How does the throttling pattern protect services from burst traffic — what is the difference between server-side rate limiting (rejecting excess requests with 429) and client-side backoff (reducing request rate in response to throttle signals), and how does throttling interact with retry logic and circuit breakers to form a complete overload protection strategy?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>17. How does backpressure differ from throttling and rate limiting as a flow control mechanism — how does a consumer signal a producer to slow down, why is queue depth a key backpressure signal, and what happens in a system where the producer ignores backpressure signals (unbounded queue growth, OOM, cascading failures)?</summary>

<!-- Answer will be added later -->

</details>

## Practical — Implementation & Composition

<details>
<summary>18. Implement a circuit breaker in TypeScript that wraps an async function call — it should track failures, transition through closed/open/half-open states, compose with a retry mechanism (retry on transient errors before tripping the breaker), and use bulkhead-style concurrency limiting to cap the number of in-flight requests to a downstream service. Show the code and explain how the three patterns interact.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>19. Implement a retry utility in TypeScript that supports exponential backoff with full jitter — it should accept a maximum retry count, a base delay, distinguish between retryable and non-retryable errors (based on error type or HTTP status code), and include a total timeout budget that aborts retries when the budget is exhausted. Show the code and explain why full jitter is better than equal jitter or no jitter.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>20. Implement a saga orchestrator in TypeScript for a multi-step workflow (e.g., reserve inventory, charge payment, send confirmation) — each step has an execute function and a compensate function, the orchestrator runs steps sequentially and triggers compensating transactions in reverse order on failure, and every compensation must be idempotent. Show the code and explain how you'd persist saga state for crash recovery.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>21. Implement cache-aside with stampede prevention in TypeScript using Redis — show a `getOrSet` function that checks the cache first, acquires a lock (using `SET NX EX`) on cache miss to prevent multiple concurrent callers from hitting the database simultaneously, and falls back gracefully if the lock can't be acquired. Explain why a naive cache-aside without locking causes stampedes under high concurrency.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>22. Implement a simplified CQRS setup in TypeScript — show a write model that processes commands and emits domain events, a read model (materialized view) that consumes those events and maintains a denormalized projection optimized for queries, and explain how eventual consistency manifests (what the user sees immediately after a write vs after projection catches up).</summary>

<!-- Answer will be added later -->

</details>

## Practical — Scenario & Design

<details>
<summary>23. Design timeout budget propagation across a three-service call chain in TypeScript — Service A receives a request with a 5-second deadline, calls Service B which calls Service C. Show how each service calculates the remaining budget (subtracting elapsed time and local processing overhead), passes it to the next service via headers or context, and how the deepest service uses the remaining budget for its own downstream calls. What happens when the budget is already exhausted before a call is made?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>24. Implement health check endpoints for a Node.js/Express service that serves both a liveness probe and a readiness probe — the liveness check should verify the process is responsive, the readiness check should verify the database connection and a critical downstream dependency are healthy. Show the code, explain why a database check should NOT be in the liveness probe, and how to implement a circuit breaker around the dependency check to prevent the health check itself from timing out.</summary>

<!-- Answer will be added later -->

</details>

---

## Experience-Based Questions

These questions test real-world experience. Prepare by mapping them to your own projects and situations.

<details>
<summary>25. Tell me about a time you implemented a circuit breaker, retry, or timeout pattern in production — what problem triggered the need, how did you choose the thresholds, and what did you learn about tuning these patterns for real traffic?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>26. Describe a time you dealt with a cascading failure in a distributed system — what were the symptoms, how did you diagnose the root cause, and what patterns or architectural changes did you implement to prevent it from happening again?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>27. Describe a time you decided a design pattern was overkill and chose a simpler approach — or a time you regretted not applying a pattern sooner. What was the situation, how did you make the decision, and what did you learn about when patterns earn their complexity?</summary>

<!-- Answer framework will be added later -->

</details>
