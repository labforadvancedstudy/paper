# Variable

## Core Insight
The named box that holds changing values, the fundamental unit of state in computation.

Variables are the primary abstraction for storing and manipulating data in programs. They represent locations in memory that can hold values, and these values can change over time as the program executes. A variable is both a name and a container - the name provides human-readable access to a memory location, while the container holds the actual data.

The power of variables lies in their mutability. Unlike mathematical variables which represent fixed unknowns, programming variables are dynamic storage locations. They allow programs to remember things, accumulate results, and respond to changing conditions. Without variables, programs would be purely functional transformations with no memory or state.

Variables introduce time into programming. Each assignment creates a new moment in the program's execution history. The same variable name can hold different values at different points in time, creating a temporal dimension in code. This temporal aspect is both powerful and dangerous - it enables complex behaviors but also introduces bugs related to unexpected state changes.

Modern programming languages provide various forms of variables: mutable and immutable, local and global, strongly and weakly typed. Each form represents different trade-offs between flexibility and safety, performance and correctness.

## Connections
→ [[state]]
→ [[function]]
→ [[data_structure]]
← [[code]]

---
Level: L1
Date: 2025-06-21
Tags: #fundamental #state #memory #naming