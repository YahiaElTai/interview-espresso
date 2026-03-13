# System Design: Chat System

> **18 questions**

- Requirements and estimation: daily message volume, peak concurrent WebSocket connections, storage growth per year, read-to-write ratio, bandwidth per connection
- API design: REST endpoints and WebSocket event schemas
- Data models: users, conversations (1:1 and group), messages, read receipts
- High-level architecture: API gateway, chat service, presence service, notification service, message store
- WebSocket vs long polling vs SSE vs HTTP polling for real-time delivery
- Message flow: end-to-end 1:1 delivery, offline user handling
- Group messaging: fan-out on write vs read, small vs large group strategies, roles, permissions, membership changes
- Message storage: NoSQL (Cassandra, DynamoDB) partition/sort key design, pagination
- Message routing: centralized connection registry (Redis), pub/sub, consistent hashing
- Message ordering: per-conversation ordering, sequence numbers, server-assigned timestamps
- Delivery guarantees: sent/delivered/read, at-least-once, idempotency keys, deduplication
- WebSocket gateway: connection lifecycle, JWT auth handshake, heartbeats, reconnection
- Read receipts, typing indicators, and unread counts: event flow, per-user read positions, throttling for large groups
- Scaling WebSocket servers: graceful draining, sticky sessions vs connection registry
- Failure scenarios: gateway failure (reconnection + catch-up), message store unavailability (write-ahead queue, retry), presence service crash (graceful degradation, stale state TTL)

---

## Requirements & Estimation

<details>
<summary>1. You're asked to design a chat system like WhatsApp or Slack — how do you gather functional and non-functional requirements, and how do you estimate message volume, concurrent WebSocket connections, storage growth per year, and bandwidth needs to establish the scale constraints that will drive every architectural decision?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>2. Design the API surface for a chat system — what REST endpoints do you need for non-real-time operations (user management, conversation CRUD, message history), what WebSocket event schemas handle real-time communication (send message, receive message, typing, presence updates), and why do you split the API this way instead of putting everything over WebSocket or everything over REST?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>3. Design the core data models for users, conversations (supporting both 1:1 and group chats), messages, and read receipts — what fields does each entity need, how do you model the relationship between conversations and participants, and why does the choice of 1:1 vs group conversation model affect schema design decisions downstream (e.g., should 1:1 chats be a special case of group chats or a separate model)?</summary>

<!-- Answer will be added later -->

</details>

## High-Level Architecture

<details>
<summary>4. Sketch the high-level architecture of a chat system showing the API gateway, chat service, presence service, notification service, and message store — why does each component exist as a separate service instead of being combined, what are the communication patterns between them, and what would you lose by merging any two of these components?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. Compare WebSocket, long polling, Server-Sent Events (SSE), and HTTP polling for real-time message delivery in a chat system — what are the tradeoffs of each in terms of latency, server resource usage, connection overhead, and bidirectional communication, why do most production chat systems choose WebSocket, and when might you still need a fallback transport?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. Walk through the end-to-end flow of a 1:1 message from the moment User A hits send to the moment User B sees it on screen — cover every service the message passes through, where it gets persisted, how the recipient's connection is located, and what happens differently when User B is offline (how does the message get stored for later delivery and how does User B eventually receive it)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. Design the WebSocket gateway layer — how does a client establish a WebSocket connection (including JWT authentication during the handshake), what is the full connection lifecycle (connect, authenticate, subscribe, heartbeat, disconnect), why are heartbeats necessary even though TCP has keepalive, and how should the client handle reconnection after a dropped connection (including catching up on missed messages)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. How does the system route a message to the correct WebSocket server when the recipient could be connected to any server in the fleet — design a message routing layer using a centralized connection registry in Redis, explain how pub/sub enables cross-server delivery, and why might you use consistent hashing to assign users to gateway servers instead of (or in addition to) a registry lookup?</summary>

<!-- Answer will be added later -->

</details>

## Component Deep Dives

<details>
<summary>9. For group messaging, compare fan-out on write (pre-computing each member's inbox at send time) vs fan-out on read (writing once and resolving recipients at read time) — what are the tradeoffs in write amplification, read latency, and storage cost, why do most systems use different strategies for small groups vs large groups (e.g., channels with thousands of members), and where is the typical threshold?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>10. How do you model group roles (admin, member, owner), permissions (who can post, pin messages, add members), and membership changes (joins, leaves, kicks) — what fields and relationships does the data model need, how does the application layer enforce permissions, and what are the tradeoffs of checking permissions at the gateway vs at the chat service?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>11. What happens to message delivery when a group member is added or removed mid-conversation — how do you decide which messages the new member can see (full history vs from-join-point), how do you prevent race conditions where a kicked user sends a message before the membership change propagates, and what consistency guarantees does the system need for membership operations?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. Design the message storage layer using a NoSQL database like Cassandra or DynamoDB — how do you choose the partition key and sort key to support the primary access pattern (fetch messages for a conversation in reverse chronological order), how does cursor-based pagination work for chat history, and what are the tradeoffs of partitioning by conversation_id vs by user_id for different read patterns?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. How do you ensure messages appear in the correct order within a conversation — why can't you rely solely on client timestamps, how do server-assigned timestamps or per-conversation sequence numbers solve this, what happens when two messages arrive at the server simultaneously, and how does ordering become harder in distributed or multi-region setups where multiple servers handle the same conversation?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>14. Design the delivery guarantee system that tracks message states (sent, delivered, read) — how does the server confirm delivery to the client, why do you need at-least-once delivery semantics with idempotency keys and client-side deduplication rather than exactly-once, and what is the concrete flow when a message is sent but the ACK is lost (how does the client retry without the recipient seeing duplicates)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>15. Design the read receipt and unread count features — what events flow between clients and the server when a user reads a message, how do you track per-user read positions within a conversation efficiently (without writing a row per user per message), how do unread counts get calculated from read positions, and how do these features degrade in large groups where fan-out of read receipts becomes expensive?</summary>

<!-- Answer will be added later -->

</details>

## Scaling & Failure Handling

<details>
<summary>16. How do you scale a fleet of WebSocket gateway servers — why is scaling stateful WebSocket connections fundamentally different from scaling stateless HTTP services, how does graceful connection draining work during deployments (move connections without dropping messages), and what are the tradeoffs of sticky sessions (routing a user to the same server) vs a connection registry (any server can route to any user)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>17. A WebSocket gateway server crashes and 50,000 users lose their connections simultaneously — walk through what happens: how do clients detect the failure and reconnect, how does the connection registry get cleaned up (stale entries), how do messages sent during the outage get buffered and delivered, and what design choices prevent this from cascading into a "thundering herd" that crashes other gateway servers?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>18. The message store (e.g., Cassandra cluster) becomes temporarily unavailable — how does the system degrade gracefully so users can still send and receive real-time messages even if chat history is inaccessible, what buffering or write-ahead strategies prevent message loss during the outage, and how do you reconcile buffered messages once the store recovers?</summary>

<!-- Answer will be added later -->

</details>

