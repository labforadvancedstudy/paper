# Code as Communication
## Core Insight
Code is written once but read many times - optimize for human understanding, not computer execution.

## The Audience Hierarchy

Code communicates to:
1. **Future you** (most important)
2. **Team members** (collaboration)
3. **Future maintainers** (legacy)
4. **The computer** (least important)

Humans first, machines second.

## Clarity Principles

**Explicit over implicit**
```python
# Bad
x = d * 24 * 60 * 60

# Good
seconds_per_day = 24 * 60 * 60
total_seconds = days * seconds_per_day
```

**Intention-revealing names**
```python
# Bad
def calc(x, y):
    return x * y * 0.1

# Good
def calculate_discount_amount(price, quantity):
    DISCOUNT_RATE = 0.1
    return price * quantity * DISCOUNT_RATE
```

**Single responsibility**
Each function/class does one thing well.

## Documentation Levels

**Code**: Self-documenting names
**Comments**: Why, not what
**Docstrings**: Contract and usage
**README**: Project overview
**Wiki**: Deep knowledge

Each level serves different needs.

## The Paradox

Best code needs no comments.
Real code needs explanation.
Balance clarity with pragmatism.

## Code as Literature

Great code reads like prose:
- Clear narrative flow
- Consistent voice
- Proper pacing
- Meaningful structure

Programming is writing for humans.

## Connections
→ [[054_code_as_language]] (philosophical depth)
→ [[038_refactoring]]
→ [[023_testing]]
← [[005_emergent_architecture]]

---
Level: L6
Date: 2025-06-21
Tags: #communication #readability #documentation #clarity