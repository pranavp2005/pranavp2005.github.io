---
title: "Linear PBFT"
order: 2
collection: portfolio
excerpt: "A replicated banking service implementing Linear PBFT (collector-based BFT) with PBFT view-change for Byzantine fault tolerance."
teaser: projects/pbft.png
header:
  teaser: projects/pbft.png
---

A fault-tolerant banking application using **Linear PBFT** for **state machine replication** in the presence of Byzantine faults. Linear-PBFT replaces PBFT’s quadratic all-to-all phases with a **collector-based linear communication pattern**, while keeping **PBFT view-change** to safely recover from faulty leaders.

- GitHub: [Linear PBFT](https://github.com/pranavp2005/ProjectShowcase/tree/main/CSE535-DistributedSystems/BFT)
- Demo: TODO (optional)

Notes
=====

## What I built

### Replicated banking state machine
- **Transfer (write)** operations that go through consensus
- **Balance (read-only)** operations that can be served via a replica fast-path with quorum replies

### Linear-PBFT normal case
- Leader assigns order (sequence numbers) and coordinates progress
- Replicas send signed votes to a **collector**; the collector aggregates a quorum (**n−f signed messages**) and broadcasts them in one message to all replicas to keep communication linear

### PBFT view-change
- On suspected leader failure (timeouts), replicas exchange **view-change** messages
- The next leader forms a **new-view** after collecting **2f+1 view-change** messages, ensuring safety across views

## Threat model / faults tolerated
- **Byzantine replicas and clients**, assuming cryptography holds (messages are signed and validated)

Tested adversarial behaviors, including:
- Invalid signature / authentication failures
- Crash / “no-send” behaviors (leader or backups)
- Selective omission (“in-dark”) toward honest replicas
- Timing delays by a malicious leader
- Equivocation (conflicting ordering info to different replica subsets)

## Debuggability / observability
Terminal tooling to inspect:
- per-node request logs (`PrintLog`)
- datastore state (`PrintDB`)
- per-sequence status across nodes (`PrintStatus`: `PP/P/C/E/X`)
- view history (`PrintView`: all new-view messages observed)
