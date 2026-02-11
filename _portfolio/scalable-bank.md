---
title: "Scalable Bank"
order: 1
collection: portfolio
excerpt: "Scalable fault-tolerant banking using 2 Phase Commit for cross-shard operations and multi-paxos for fault tolerance."
teaser: projects/scalable-bank.png
header:
  teaser: projects/scalable-bank.png
---

A scalable fault-tolerant banking application using **Multi-Paxos** for **state machine replication**, with **dynamic sharding** based on workload and **2PC** for cross-shard transfers. Includes a **configurable cluster setup** and **configurable read consistency** (linearizable / quorum / eventual). Peak throughput: **~6,000 transactions/sec**.

- GitHub: [Scalable Fault-tolerant banking service using 2PC and Multi-paxos](https://github.com/pranavp2005/ProjectShowcase/tree/main/CSE535-DistributedSystems/2PC)
- Demo: TODO (optional)

Notes
=====

What I built
------------
A sharded, replicated banking service that supports:
- **Balance(s)**: read-only query for account `s`
- **Transfer(s, r, amt)**:
  - **Intra-shard** if `s` and `r` are in the same shard: replicated + executed via **Multi-Paxos** within that shard.
  - **Cross-shard** if `s` and `r` are in different shards: executed using **2PC across shards**, with **Multi-Paxos inside each shard** to keep replicas consistent.

Configurable cluster (bonus)
----------------------------
Made the deployment configurable to vary:
- number of **shards**
- number of **replicas per shard**
This allowed benchmarking different scale-out configurations and failure scenarios on the same codebase.

Read consistency modes
----------------------
Implemented configurable read consistency for `Balance`:
- **Linearizable reads**: strongest guarantee (reads reflect the latest committed write).
- **Quorum reads**: query a quorum of replicas and return the latest value among them.
- **Eventual reads**: read from a single replica (fastest, may be stale).

2PC flow (cross-shard transfer)
-------------------------------
For a cross-shard transfer `(s, r, amt)`:
1. **Coordinator shard** = shard that owns sender `s`. Its leader:
   - checks `s` is unlocked and has sufficient funds
   - locks `s`
   - sends **PREPARE** to participant shard (owner of `r`)
   - replicates the prepare decision via **Multi-Paxos**, writing undo information to **WAL**

2. **Participant shard** leader:
   - checks `r` is unlocked
   - locks `r`
   - replicates its prepare decision via **Multi-Paxos**
   - replies **PREPARED** if successful, else **ABORT**

3. If both shards are prepared:
   - coordinator sends **COMMIT** (or **ABORT** on timeout/failure)
   - both shards replicate the final decision via **Multi-Paxos**
   - on commit: apply updates + release locks + clear WAL entries
   - on abort/timeout: use WAL to **undo** partial work, then release locks

Sharding strategy + rebalancing
-------------------------------
- Start with a fixed shard mapping (range partitioning).
- Periodically compute an improved mapping from transaction history to:
  - **reduce cross-shard transfers** (co-locate frequently co-accessed records)
  - keep shards **balanced**
- Model history as a hypergraph: **records = vertices**, **transactions = hyperedges**; partition into balanced groups to minimize cross-partition edges.
- Perform **offline data movement** and output moved records as triplets like `(recordId, sourceShard, destShard)`.

Benchmarking
------------
- Workload generator knobs:
  - read-only vs read-write ratio
  - intra-shard vs cross-shard ratio
  - hotspot skew (hot keys) to stress contention
- Measured client-perceived latency/throughput; achieved **~6,000 TPS peak throughput** under tuned settings.
