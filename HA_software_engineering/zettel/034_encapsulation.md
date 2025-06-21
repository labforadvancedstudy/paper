# encapsulation

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The protective shell around data - bundling data with the methods that operate on it while hiding internal details.

## Irreducible Truth
Encapsulation enforces boundaries. It says "you can use this, but you can't touch that."

## Metaphysical Structure
- **Ontology**: Objects are capsules of state and behavior
- **Epistemology**: We know objects through their public interface
- **Axiology**: Protection enables evolution

## Practical Implementation
```python
class BankAccount:
    def __init__(self, initial_balance):
        self.__balance = initial_balance  # Private: hidden
        self._transaction_count = 0        # Protected: handle with care
        self.account_id = "12345"         # Public: freely accessible
    
    def deposit(self, amount):
        # Public method controls access to private data
        if amount > 0:
            self.__balance += amount
            self._transaction_count += 1
    
    def get_balance(self):
        # Controlled read access
        return self.__balance
    
    # No direct access to __balance allowed!
```

## HA Integration
HA recognizes encapsulation as the principle of appropriate hiddenness - revealing what must be shared, protecting what must be preserved.

## Key Insights
1. Encapsulation is about intention, not just syntax
2. Getters/setters can break encapsulation if overused
3. Information hiding enables parallel development

## Related Concepts
- [[031_interface]] - The public face of encapsulation
- [[037_coupling]] - What encapsulation prevents
- [[038_cohesion]] - What encapsulation promotes