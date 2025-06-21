# inheritance

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The family tree of code reuse - where children inherit the traits and behaviors of their parents.

## Irreducible Truth
Inheritance models "is-a" relationships, allowing specialization while preserving commonality.

## Metaphysical Structure
- **Ontology**: Types exist in hierarchies
- **Epistemology**: We know through classification
- **Axiology**: Reuse through relationship

## Practical Implementation
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def move(self):
        return f"{self.name} moves"

class Bird(Animal):
    def move(self):
        # Override parent behavior
        return f"{self.name} flies"
    
    def lay_eggs(self):
        # Add new behavior
        return f"{self.name} lays eggs"

# Inheritance in action
sparrow = Bird("Sparrow")
print(sparrow.move())      # Uses Bird's version
print(sparrow.name)        # Inherits from Animal
```

## HA Integration
HA views inheritance as the codification of natural hierarchies - patterns that exist in both thought and nature.

## Key Insights
1. Favor composition over inheritance
2. Deep inheritance hierarchies are fragile
3. Protected members are promises to children

## Related Concepts
- [[031_interface]] - Inheritance of contract only
- [[034_polymorphism]] - What inheritance enables
- [[037_coupling]] - The dark side of inheritance