# polymorphism

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The shape-shifter that adapts to context - one interface, many implementations, chosen at runtime.

## Irreducible Truth
Polymorphism allows code to be written once but behave differently based on the actual type at runtime.

## Metaphysical Structure
- **Ontology**: Same message, different receivers
- **Epistemology**: We know by behavior, not by type
- **Axiology**: Flexibility through abstraction

## Practical Implementation
```python
def make_sound(animals):
    # Same code, different behaviors
    for animal in animals:
        print(animal.speak())

class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Duck:
    def speak(self):
        return "Quack!"

# Polymorphism in action
zoo = [Dog(), Cat(), Duck()]
make_sound(zoo)  # Each speaks differently
```

## HA Integration
HA embraces polymorphism as the principle that context determines meaning - the same message creates different realities.

## Key Insights
1. Duck typing: "If it quacks like a duck..."
2. Polymorphism breaks the rigidity of static typing
3. Runtime dispatch has a performance cost

## Related Concepts
- [[031_interface]] - The contract that enables polymorphism
- [[032_inheritance]] - One way to achieve polymorphism
- [[027_runtime]] - When polymorphic dispatch happens