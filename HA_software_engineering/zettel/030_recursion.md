# recursion

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The function that solves problems by asking itself - the computational mirror that reflects smaller versions of the same problem.

## Irreducible Truth
Recursion proves that complex problems often have simple, self-similar structures.

## Metaphysical Structure
- **Ontology**: Recursion is self-reference with termination
- **Epistemology**: We understand through decomposition
- **Axiology**: Elegance through self-similarity

## Practical Implementation
```python
def factorial(n):
    # Base case: the mirror's edge
    if n <= 1:
        return 1
    # Recursive case: look deeper into the mirror
    return n * factorial(n - 1)

# The call stack builds a tower of self-reference:
# factorial(5) -> 5 * factorial(4)
#              -> 5 * 4 * factorial(3)
#              -> 5 * 4 * 3 * factorial(2)
#              -> 5 * 4 * 3 * 2 * factorial(1)
#              -> 5 * 4 * 3 * 2 * 1
```

## HA Integration
HA recognizes recursion as a fundamental pattern of understanding - we comprehend wholes by understanding parts that resemble the whole.

## Key Insights
1. Every recursive solution has an iterative equivalent
2. The base case prevents infinite self-reference
3. Tail recursion optimizes away the call stack

## Related Concepts
- [[028_memory]] - Stack overflow from deep recursion
- [[006_loop]] - The iterative alternative
- [[016_abstraction]] - Recursion as ultimate abstraction