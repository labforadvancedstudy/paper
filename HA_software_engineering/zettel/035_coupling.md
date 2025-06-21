# coupling

**Level**: L3  
**Domain**: Software Engineering

## Core Concept
The web of dependencies between components - the invisible strings that make change difficult.

## Irreducible Truth
Coupling is inevitable; the question is whether it's appropriate. Zero coupling means zero functionality.

## Metaphysical Structure
- **Ontology**: Relationships create complexity
- **Epistemology**: We know coupling by counting dependencies
- **Axiology**: Loose coupling enables evolution

## Practical Implementation
```python
# Tight coupling - classes know too much about each other
class EmailSender:
    def send(self, user):
        smtp = SMTPConnection("smtp.gmail.com", 587)
        smtp.login("hardcoded@gmail.com", "password123")
        smtp.send(user.email, f"Hello {user.first_name}")

# Loose coupling - dependency injection
class EmailSender:
    def __init__(self, smtp_connection, template_engine):
        self.smtp = smtp_connection
        self.templates = template_engine
    
    def send(self, user, template_name):
        message = self.templates.render(template_name, user)
        self.smtp.send(user.email, message)
```

## HA Integration
HA treats coupling as the measure of systemic brittleness. Appropriate coupling creates resilient systems.

## Key Insights
1. Coupling is a spectrum, not binary
2. Temporal coupling (order dependencies) is often hidden
3. The law of Demeter: talk to friends, not strangers

## Related Concepts
- [[036_cohesion]] - The counterbalance to coupling
- [[034_encapsulation]] - Defense against coupling
- [[039_modularity]] - Architecture to manage coupling