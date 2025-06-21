# The Art of Abstraction
## Core Insight
Great software engineering is the art of finding the right level of abstraction - not too specific, not too general.

## The Abstraction Hierarchy

```
Machine Code
    ↑
Assembly
    ↑
System Calls
    ↑
Libraries
    ↑
Frameworks
    ↑
Applications
    ↑
Domain Languages
```

Each level hides complexity below, enables expression above.

## The Goldilocks Principle

**Too Low**: 
- Drowning in details
- Reinventing wheels
- Error prone
- Slow development

**Too High**:
- Lost flexibility
- Performance penalties
- Leaky abstractions
- Magic syndrome

**Just Right**:
- Essential complexity visible
- Accidental complexity hidden
- Power with control
- Understanding preserved

## Abstraction Patterns

**Encapsulation**: Hide implementation
**Interface**: Define contract
**Composition**: Build from parts
**Inheritance**: Share structure
**Polymorphism**: Many forms
**Generics**: Type abstraction

Each pattern: A way of forgetting wisely.

## The Leaky Reality

All abstractions leak:
- Performance surprises
- Edge cases emerge
- Assumptions break
- Reality intrudes

Good engineers know when to break abstraction.

## Connections
→ [[021_design_pattern]]
→ [[031_interface]]
→ [[034_encapsulation]]
← [[001_software_essence]]
← [[014_abstraction]] (philosophical perspective)

---
Level: L2
Date: 2025-06-21
Tags: #abstraction #design #patterns #architecture