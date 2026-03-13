# Networking & Protocols

> **18 questions** — 13 theory, 5 practical

- End-to-end request lifecycle: DNS resolution, TCP connect, TLS handshake, HTTP request/response — the full path of a network call
- TCP/IP model: application, transport, network, link layers — encapsulation, data flow, and how layering guides debugging
- TCP reliability: three-way handshake, teardown, sequence numbers, sliding window, flow control, congestion control basics (slow start)
- UDP vs TCP tradeoffs and which protocols build on each
- DNS resolution: recursive vs iterative queries, caching, TTL, failure modes
- HTTP/1.1 vs HTTP/2 vs HTTP/3: head-of-line blocking, multiplexing, binary framing, HTTP/3 over QUIC (UDP-based, connection migration)
- HTTP semantics: method idempotency (GET/PUT/DELETE vs POST), status code families, commonly misused codes (401 vs 403, 502 vs 503), retry-safe vs non-retry-safe responses
- gRPC: HTTP/2 transport, Protobuf serialization, streaming modes (unary, server, client, bidirectional), and tradeoffs vs REST
- WebSockets vs SSE vs HTTP polling: upgrade handshake, frames, persistent connection models (keep-alive vs multiplexing vs WebSocket), operational costs, when each fits
- Proxies and load balancers: L4 vs L7 differences, X-Forwarded-For/X-Real-IP headers, TLS termination points, and how proxies affect client IP visibility
- HTTP caching: Cache-Control, ETag, Vary, conditional requests, cache poisoning
- CORS: preflight mechanism, credentialed requests, common misconfigurations and wildcard pitfalls

---

## Foundational

<details>
<summary>1. What happens end-to-end when a browser makes an HTTPS request — walk through the full lifecycle from DNS resolution through TCP connection, TLS handshake, and HTTP request/response, explaining what each step accomplishes and why the sequence matters for understanding latency and failure modes?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>2. Why is the TCP/IP model organized into layers (application, transport, network, link) instead of being a single monolithic protocol — what problem does layering solve, how does encapsulation work as data moves through the stack, and how does understanding layers help you debug networking issues faster?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>3. Why do both TCP and UDP exist instead of just one transport protocol — what are the fundamental tradeoffs between reliability and performance, which well-known protocols build on each (and why), and when would you deliberately choose UDP over TCP in a backend system?</summary>

<!-- Answer will be added later -->

</details>

## Conceptual Depth

<details>
<summary>4. How does TCP establish and tear down connections reliably -- explain the three-way handshake and four-way teardown, what sequence numbers and acknowledgments accomplish, and why the protocol needs both a connection setup and an explicit teardown phase rather than just sending data directly?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. How do TCP's flow control and congestion control mechanisms prevent network collapse -- explain the sliding window mechanism, how flow control prevents the sender from overwhelming the receiver, and how congestion control (slow start, congestion avoidance) adapts to network capacity, including why these are separate mechanisms solving different problems?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. How does DNS resolution actually work — what is the difference between recursive and iterative queries, how does caching at each level (browser, OS, resolver, authoritative) interact with TTL values, and what are the common DNS failure modes that cause outages in production (stale caches, propagation delays, resolver failures)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. Why did the web need HTTP/2 and HTTP/3 when HTTP/1.1 worked for decades — explain head-of-line blocking at the HTTP level (HTTP/1.1) vs at the TCP level (HTTP/2), how HTTP/2's binary framing and multiplexing solve the first problem, and why HTTP/3 had to move to QUIC over UDP to solve the second, including what connection migration enables that TCP cannot?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. Why does HTTP distinguish between safe, idempotent, and non-idempotent methods — explain how GET, PUT, DELETE, and POST differ in terms of idempotency and safety, why this matters for retry logic and caching, what the status code families (1xx-5xx) signal, and why certain codes are commonly misused (401 vs 403, 502 vs 503, 200 for errors)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>9. Why would you choose gRPC over REST for service-to-service communication — explain how gRPC uses HTTP/2 as its transport, why Protobuf serialization matters for performance and type safety, what the four streaming modes (unary, server streaming, client streaming, bidirectional) enable, and what the real-world tradeoffs are (tooling, debugging, browser support, learning curve)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>10. When would you choose WebSockets vs Server-Sent Events vs HTTP long polling for a real-time feature -- explain how each approach works at a high level (WebSocket upgrade and full-duplex frames, SSE over standard HTTP, polling's simplicity), what the operational costs are for each (connection limits, load balancer stickiness, reconnection handling), and what factors drive the decision in practice?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>11. What is the difference between an L4 and L7 load balancer/proxy, why does the layer matter — explain what each layer can inspect and route on, where TLS termination typically happens (and the tradeoffs of terminating at the proxy vs the backend), how X-Forwarded-For and X-Real-IP headers preserve client IP visibility through proxy chains, and what breaks when these headers are missing or misconfigured?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. How does HTTP caching work end-to-end — explain the Cache-Control directives (max-age, no-cache, no-store, public/private, s-maxage), how ETag and Last-Modified enable conditional requests (304 Not Modified), what the Vary header does and why it matters for CDNs, and how cache poisoning attacks exploit caching infrastructure?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. Why does CORS exist and how does the preflight mechanism actually work — explain what the browser enforces vs what the server controls, how OPTIONS preflight requests work, why credentialed requests have stricter rules (no wildcard origins), and what the common CORS misconfigurations are that either break legitimate requests or create security vulnerabilities?</summary>

<!-- Answer will be added later -->

</details>

## Practical — Implementation & Configuration

<details>
<summary>14. Configure CORS middleware in a Node.js/Express API that handles both simple and preflighted requests — show the middleware setup for allowing specific origins, handling credentialed requests, exposing custom headers, and explain what breaks when you use a wildcard origin with credentials and how you'd support multiple allowed origins dynamically?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>15. Implement a Server-Sent Events endpoint in Node.js and a basic WebSocket server for the same use case (e.g., live notifications) — show both implementations side by side, explain the key differences in setup complexity, connection handling, and how the client reconnects after disconnection in each approach?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>16. Set appropriate Cache-Control headers in a Node.js API for three scenarios: static assets (JS/CSS with content hashes), public API responses that change infrequently, and user-specific data that must not be cached by shared caches — show the middleware configuration and explain why each directive combination is correct for its scenario?</summary>

<!-- Answer will be added later -->

</details>

---

## Experience-Based Questions

These questions test real-world experience. Prepare by mapping them to your own projects and situations.

<details>
<summary>17. Tell me about a time you debugged a networking issue in production — what were the symptoms, what tools did you use to isolate the problem, and what turned out to be the root cause?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>18. Tell me about a time you had to choose between WebSockets, SSE, and HTTP polling for a real-time feature — what were the requirements, what tradeoffs did you evaluate, and would you make the same choice again?</summary>

<!-- Answer framework will be added later -->

</details>

