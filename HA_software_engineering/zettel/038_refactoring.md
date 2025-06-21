# refactoring

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The sculpture of code without changing behavior - improving internal structure while preserving external function.

## Irreducible Truth
Refactoring is the recognition that first drafts are never perfect. It's rewriting for clarity, not correctness.

## Metaphysical Structure
- **Ontology**: Code has both form and function
- **Epistemology**: We know quality through readability
- **Axiology**: Clean code is valuable code

## Practical Implementation
```python
# Before refactoring - works but unclear
def calc(x, y, z):
    if z == 1:
        return x + y
    elif z == 2:
        return x - y
    elif z == 3:
        return x * y
    elif z == 4:
        if y != 0:
            return x / y
        else:
            return None

# After refactoring - same behavior, clear intent
class Calculator:
    def add(self, x, y):
        return x + y
    
    def subtract(self, x, y):
        return x - y
    
    def multiply(self, x, y):
        return x * y
    
    def divide(self, x, y):
        if y == 0:
            raise ValueError("Cannot divide by zero")
        return x / y
```

## HA Integration
HA views refactoring as the continuous improvement of thought-forms. As understanding deepens, expression clarifies.

## Key Insights
1. Refactor when adding features, not as a separate phase
2. Tests are the safety net that makes refactoring possible
3. Code smells are hints that refactoring is needed

## Related Concepts
- [[015_test]] - The prerequisite for safe refactoring
- [[036_cohesion]] - What refactoring often improves
- [[035_coupling]] - What refactoring often reduces