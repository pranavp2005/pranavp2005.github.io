---
title: "Multi Paxos"
collection: portfolio
excerpt: "A crash fault-tolerant banking app using Multi-Paxos for state machine replication."
teaser: projects/multi-paxos.png
header:
  teaser: projects/multi-paxos.png
---

A fault-tolerant banking application using **Stable-Leader Paxos (Multi-Paxos)** for **state machine replication**, implemented in **Go** using **RPC**.

Implemented a **Multi-Paxos–inspired stable-leader consensus protocol** in **Go** using **RPC**, and applied it to a **replicated banking service** using **state machine replication**. The focus was to keep replicas consistent while processing a stream of transactions, and to recover cleanly and safely when the leader crashes.

- GitHub: [Multi-Paxos Project (Go, RPC)](https://github.com/pranavp2005/ProjectShowcase/tree/main/CSE535-DistributedSystems/CFT/Project01)
- Demo: TODO

Notes
=====

Highlights
----------
- **Total-order replication:** Assigned each transaction a **sequence number** and enforced in-order execution to keep replica state identical.
- **Stable-leader fast path:** After leader election, drove **ACCEPT → ACCEPTED → COMMIT** using **majority quorums**, then executed and replied to the client.
- **View change & recovery:** On leader failure, collected **AcceptLogs** via **PREPARE/ACK**, published **NEW-VIEW** with the best-known accepted value per slot, and inserted **no-ops** to safely fill gaps.
- **Exactly-once semantics:** Used **monotonic client timestamps** and **per-client response caching** to prevent duplicate execution under retries/timeouts.
- **Debuggability:** Added CLI introspection commands to inspect correctness and progress (**PrintLog**, **PrintDB**, **PrintStatus(seq)**, **PrintView**).

Failure validation
----------------
Validated safety and liveness under:
- **Leader failure** during active traffic
- **Backup replica failure** (progress maintained as long as failures ≤ *f*)
- **Consecutive leader failures** across multiple views

What I learned
--------------
This project made consensus concrete: how quorums translate into safety, why log recovery must be precise, how ordering constraints shape the implementation, and why strong observability is essential when validating correctness under failures.
