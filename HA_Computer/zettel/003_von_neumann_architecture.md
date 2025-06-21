# Von Neumann Architecture
## Core Insight
Stored program concept - instructions and data in same memory, making computers universal machines.

## The Breakthrough (1945)

Before Von Neumann:
- Hardwired programs
- Fixed functionality
- Separate data/instruction storage

After:
- Programs are data
- Self-modifying code possible
- Universal computation practical

## The Architecture

```
CPU ←→ Memory ←→ I/O
 ↓
Control Unit + ALU
```

**CPU**: Fetches, decodes, executes
**Memory**: Stores both data and instructions
**Bus**: Connects components
**I/O**: Interfaces with world

## The Von Neumann Bottleneck

Problem: CPU waits for memory
- Fast processor
- Slow memory access
- Single bus limitation
- Sequential operation

Solutions attempted:
- Cache hierarchies
- Parallel architectures
- Harvard architecture
- Quantum approaches

## Why It Persists

Despite limitations:
- Simple to understand
- Easy to program
- Proven reliable
- Economically efficient
- Conceptually elegant

Most computers still Von Neumann at core.

## The Philosophical Depth

Programs as data means:
- Code can examine code
- Systems can evolve
- Computation becomes recursive
- Mirrors consciousness?

## Connections
→ [[009_stored_program]]
→ [[010_cpu_design]]
→ [[011_memory_hierarchy]]
← [[002_binary_reality]]

---
Level: L3
Date: 2025-06-21
Tags: #architecture #von_neumann #cpu #memory