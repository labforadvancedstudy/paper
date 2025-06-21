# error

**Level**: L1  
**Domain**: Software Engineering

## Core Concept
The honest feedback that something went wrong - a signal that reality doesn't match expectation.

## Irreducible Truth
Error is information. It tells us precisely where our mental model diverged from actual system behavior.

## Metaphysical Structure
- **Ontology**: Errors exist as first-class citizens in computation
- **Epistemology**: We know through failure what we cannot know through success
- **Axiology**: Errors have positive value as learning signals

## Practical Implementation
```python
try:
    result = risky_operation()
except ValueError as e:
    # Error becomes data
    log_error(e)
    return safe_default()
```

## HA Integration
In HA systems, errors are not failures but feedback loops that drive adaptation and learning.

## Key Insights
1. Errors are not bugs - bugs are errors we haven't handled
2. The best systems embrace errors as part of normal operation
3. Silent failure is worse than loud failure

## Related Concepts
- [[007_bug]] - The unintended behavior
- [[011_exception]] - The structured way to handle errors
- [[027_syntax]] - Where errors often first appear