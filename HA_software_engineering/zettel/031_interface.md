# interface

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The contract that hides implementation - a promise about what can be done without revealing how it's done.

## Irreducible Truth
Interfaces define the boundary between intention and implementation, enabling change without breaking promises.

## Metaphysical Structure
- **Ontology**: Interfaces are pure behavior specification
- **Epistemology**: We know components by their contracts
- **Axiology**: Good interfaces minimize coupling

## Practical Implementation
```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def process_payment(self, amount: float) -> bool:
        """The what, not the how"""
        pass

class StripeProcessor(PaymentProcessor):
    def process_payment(self, amount: float) -> bool:
        # The how for Stripe
        return self._call_stripe_api(amount)

class PayPalProcessor(PaymentProcessor):
    def process_payment(self, amount: float) -> bool:
        # The how for PayPal
        return self._call_paypal_api(amount)
```

## HA Integration
HA treats interfaces as the linguistic boundary where human intention meets machine capability. Clear interfaces enable clear communication.

## Key Insights
1. Program to interfaces, not implementations
2. Interfaces are discovered, not invented
3. The best interface is no interface

## Related Concepts
- [[033_inheritance]] - Interfaces without implementation
- [[034_polymorphism]] - What interfaces enable
- [[035_encapsulation]] - What interfaces protect