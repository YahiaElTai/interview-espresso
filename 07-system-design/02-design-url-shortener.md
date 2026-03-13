# System Design: URL Shortener

> **21 questions**

- Requirements gathering and back-of-the-envelope estimation: read/write ratio, requests per second, storage growth, bandwidth, cache memory sizing
- API design: endpoints for creation, redirection, custom aliases, expiration
- Keyspace calculation and short URL length
- Encoding strategies: base62 conversion, MD5/SHA256 hash truncation, pre-generated key service (KGS)
- Database selection: relational vs NoSQL for simple key-value access patterns
- Schema design: URL mapping table, indexes, TTL-based expiration and cleanup
- Redirect flow: 301 vs 302 tradeoffs for caching and analytics
- Caching layer: eviction policies (LRU, LFU, TTL), cache sizing for power-law traffic
- Analytics: async click tracking (geographic, referrer, device) without redirect latency
- Write path: race conditions, uniqueness checks, ID predictability mitigation
- Scaling: database sharding (key-based vs hash-based partitioning), distributed cache, stateless application servers, cache warming strategies

---

## Requirements & Estimation

<details>
<summary>1. How do you gather and prioritize functional and non-functional requirements for a URL shortener — what questions would you ask the interviewer to scope the problem, why is the read-to-write ratio the single most important characteristic to establish early, and how does it shape every subsequent design decision from caching to database choice?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>2. Walk through the back-of-the-envelope estimation for a URL shortener handling 100M new URLs per month — how do you derive reads per second from the read-to-write ratio, estimate storage growth over 5 years (including metadata), calculate cache memory requirements assuming power-law traffic distribution, and what bandwidth numbers should you sanity-check?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>3. How do you calculate the required short URL length — given a target keyspace (e.g., 100M URLs/month for 10 years), why does base62 encoding determine the minimum character count, what is the tradeoff between shorter URLs (better UX) and larger keyspace (collision safety), and at what point do you need 7 vs 8 characters?</summary>

<!-- Answer will be added later -->

</details>

## High-Level Architecture

<details>
<summary>4. Design the API contract for a URL shortener — what endpoints do you need for creation, redirection, custom aliases, and expiration, what HTTP methods and status codes are appropriate for each, why should the creation endpoint return the full short URL rather than just the key, and how do you handle optional parameters like custom aliases and TTL in the same creation endpoint?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. Compare base62 encoding of an auto-incrementing ID vs MD5/SHA256 hash truncation for generating short URLs — how does each approach work, what are the collision characteristics of each, and why does hash truncation become problematic at scale while base62 has a different set of weaknesses around sequential predictability and distributed coordination?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. What is a pre-generated key service (KGS) and why does it tend to win over base62 and hash-based approaches at scale — how does KGS avoid the collision and coordination problems of the other strategies, what infrastructure complexity does it introduce, and what is its performance profile on the write path compared to inline key generation?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. Why might you choose a relational database (PostgreSQL) vs a NoSQL store (DynamoDB, Cassandra) for the URL mapping — given that the access pattern is simple key-value lookups with a heavy read bias, what are the tradeoffs in terms of consistency guarantees, scaling characteristics, operational complexity, and how the choice changes depending on whether you need analytics joins or just fast lookups?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. Design the database schema for the URL mapping table — what columns are needed beyond the short key and long URL (think metadata, timestamps, ownership), why do you need specific indexes and what types would you choose, and how do schema decisions change depending on whether you chose a relational database vs a NoSQL store?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>9. Why is the choice between 301 (permanent) and 302 (temporary) redirects critical for a URL shortener — how does each affect browser caching behavior, CDN caching, analytics accuracy, and the ability to update or expire URLs after creation? What do most production URL shorteners actually use and why?</summary>

<!-- Answer will be added later -->

</details>

## Component Deep Dives

<details>
<summary>10. Design the caching layer for a URL shortener — why does power-law traffic distribution (a small percentage of URLs get the vast majority of clicks) make caching extremely effective, how do you size the cache (what percentage of URLs to cache and why), and what eviction policy (LRU, LFU, or TTL-based) best fits this access pattern? Walk through the read path showing cache hit vs miss flows.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>11. Design the analytics pipeline for click tracking — how do you capture geographic location, referrer, device type, and timestamp for every redirect without adding latency to the redirect response? Why is async processing essential here, what queueing or streaming architecture would you use, and how do you handle the eventual consistency between the redirect happening and the analytics data being queryable?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. Walk through the write path for creating a new short URL end-to-end — where can race conditions occur (two requests trying to claim the same key), how do you guarantee uniqueness (database constraint vs distributed lock vs KGS pre-allocation), and why is ID predictability a security concern? What attack does sequential ID exposure enable and how do you mitigate it?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. Design the KGS internals — why is a two-table approach (unused keys vs used keys) common, how does batching key allocation to application servers reduce round trips and prevent KGS from becoming a bottleneck, and what happens when a key is handed out but the URL creation subsequently fails? How do you handle key exhaustion and what monitoring would you set up to prevent it?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>14. How would you implement URL expiration end-to-end — when a user sets a TTL on a short URL, what happens at read time (check expiration before redirect vs rely on cleanup), what happens at the storage layer (lazy deletion vs scheduled cleanup job vs database-native TTL like DynamoDB's), and what are the tradeoffs of each approach in terms of storage reclamation, read latency, and complexity?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>15. How do you design the redirect flow to minimize latency — trace a request from DNS resolution through load balancer, application server, cache lookup, potential database fallback, and HTTP redirect response. Where are the latency bottlenecks, what is a realistic p50 and p99 target, and what optimizations (connection pooling, cache placement, keep-alive) shave off the most time?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>16. If you use base62 encoding of an auto-incrementing counter, how do you generate unique IDs in a distributed system — why does a single auto-increment sequence become a bottleneck, what are the options (database sequences, Snowflake-style IDs, range-based allocation), and how does each approach affect URL length, ordering, and collision safety?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>17. How do you handle the case where a hash-based encoding strategy produces a collision — walk through the collision detection and resolution flow, why does truncating MD5/SHA256 to 7 characters make collisions likely at scale, what retry or chaining strategy resolves them, and at what collision rate does this approach become impractical compared to KGS?</summary>

<!-- Answer will be added later -->

</details>

## Scaling & Failure Handling

<details>
<summary>18. How would you shard the URL database — what shard key makes sense (short URL hash vs range-based), why is the short URL key better than the long URL for sharding, how do you handle hot shards when a viral URL's analytics data concentrates on one shard, and what rebalancing strategy do you use when adding new shards?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>19. Design the distributed caching layer — why does consistent hashing matter for cache node addition/removal, how do you handle cache warming after a cold start or node failure, what is the tradeoff between cache replication (higher availability, more memory) and single-copy caching (less memory, cache miss on failure), and how do you size the cache cluster for a read-heavy workload?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>20. Why must the application tier be stateless for a URL shortener and how do you achieve this — what state (if any) do application servers hold, how does statelessness enable horizontal scaling behind a load balancer, and what load balancing strategy (round-robin, least connections, consistent hashing) works best for the read-heavy redirect traffic vs the write traffic?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>21. Put the entire design together — draw the complete architecture showing all components (clients, DNS, load balancers, app servers, KGS, cache layer, database, analytics pipeline, abuse prevention) and trace both the write path (URL creation) and read path (redirect) through the system. Identify the single points of failure and explain how each is mitigated.</summary>

<!-- Answer will be added later -->

</details>

