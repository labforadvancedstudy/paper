# cohesion

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The magnetic force that keeps related things together - how strongly the elements within a module belong with each other.

## Irreducible Truth
High cohesion means every element has a reason to be there. It's the "single reason to change" principle in practice.

## Metaphysical Structure
- **Ontology**: Unity of purpose creates strength
- **Epistemology**: We know cohesion by asking "why is this here?"
- **Axiology**: Cohesion creates comprehensibility

## Practical Implementation
```python
# Low cohesion - grab bag of unrelated functions
class Utils:
    def calculate_tax(self, amount):
        return amount * 0.08
    
    def send_email(self, to, subject):
        # Email logic
        pass
    
    def parse_csv(self, file):
        # CSV parsing
        pass

# High cohesion - everything serves one purpose
class TaxCalculator:
    def __init__(self, tax_rate):
        self.tax_rate = tax_rate
    
    def calculate_tax(self, amount):
        return amount * self.tax_rate
    
    def calculate_after_tax(self, amount):
        return amount + self.calculate_tax(amount)
    
    def calculate_tax_breakdown(self, amount):
        return {
            'pre_tax': amount,
            'tax': self.calculate_tax(amount),
            'total': self.calculate_after_tax(amount)
        }
```

## HA Integration
HA views cohesion as conceptual gravity - ideas that belong together should compute together.

## Key Insights
1. Functional cohesion > Sequential cohesion > Communicational cohesion
2. High cohesion makes modules predictable
3. The "User" class problem: when cohesion fights with data

## Related Concepts
- [[035_coupling]] - The tension with cohesion
- [[039_modularity]] - Cohesion at scale
- [[040_refactoring]] - Often aims to improve cohesion