# Distributed Systems
## Core Insight
Distributed systems turn simple problems into complex ones - but enable scale and resilience impossible in single machines.

## The Eight Fallacies

Developers assume:
1. Network is reliable
2. Latency is zero
3. Bandwidth is infinite
4. Network is secure
5. Topology doesn't change
6. One administrator
7. Transport cost is zero
8. Network is homogeneous

All false. Pain follows.

## CAP Theorem

Pick two:
- **Consistency**: All see same data
- **Availability**: System stays up
- **Partition tolerance**: Survives network splits

Reality: P happens, choose C or A.

## Distributed Patterns

**Load balancing**: Spread work
**Caching**: Remember answers
**Sharding**: Split data
**Replication**: Copy for safety
**Consensus**: Agree on truth
**Circuit breakers**: Fail fast

Each pattern trades off something.

## The Complexity Tax

Distributed adds:
- Network failures
- Partial failures
- Time synchronization
- Debugging difficulty
- Operational overhead
- Cognitive load

Sometimes monolith is right answer.

## The Beautiful Chaos

Distributed systems:
- Emergent behavior
- Self-healing
- Resilient
- Scalable
- Complex

Like consciousness - many parts, one system.

## Connections
→ [[040_distributed_system]] (metaphorical view)
→ [[041_concurrency]]
→ [[047_scalability]]
← [[006_code_as_communication]]

---
Level: L7
Date: 2025-06-21
Tags: #distributed #systems #scale #complexity