# pointer

**Level**: L2  
**Domain**: Software Engineering

## Core Concept
The signpost that points to where data lives - a reference that separates location from content.

## Irreducible Truth
Pointers embody indirection: the power to talk about data without moving data.

## Metaphysical Structure
- **Ontology**: Pointers are meta-data about data
- **Epistemology**: We know data through its address
- **Axiology**: Pointers enable efficiency through sharing

## Practical Implementation
```c
int value = 42;
int* ptr = &value;  // ptr holds the address of value

// Indirection in action
*ptr = 100;  // Change value through its address
int** ptr_to_ptr = &ptr;  // Pointers all the way down
```

## HA Integration
In HA philosophy, pointers represent the fundamental principle of reference - the ability to point at ideas without containing them.

## Key Insights
1. NULL pointers point to the absence of data
2. Pointer arithmetic is navigation through memory space
3. Smart pointers add ownership semantics to raw addresses

## Related Concepts
- [[028_memory]] - What pointers point to
- [[025_error]] - Segfaults from bad pointers
- [[032_interface]] - Pointers to functions enable polymorphism