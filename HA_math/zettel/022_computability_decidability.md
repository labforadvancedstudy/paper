# Computability and the Limits of Calculation

## Core Insight
Some mathematical questions are unanswerable not because we're not clever enough, but because no algorithm could ever answer them.

## Content
Turing's insight: let's define precisely what it means to compute. A Turing machine - infinite tape, finite states, simple rules - captures the essence of any computation.

The Church-Turing thesis claims: anything computable by any reasonable method is computable by a Turing machine. This isn't provable - it's a statement about the nature of computation itself.

Computable functions:
- Addition, multiplication: obviously computable
- Primality testing: computable (even efficiently)
- Digits of π: computable to any precision
- Solutions to polynomial equations: sometimes computable

But then the limits appear:
- Halting problem: can't tell if programs stop
- Busy beaver: grows faster than any computable function
- Kolmogorov complexity: can't compute minimal descriptions
- Diophantine equations: no general algorithm

The hierarchy of unsolvability:
- Decidable: algorithm always gives yes/no
- Semi-decidable: algorithm finds "yes" but might loop on "no"
- Undecidable: no algorithm works
- Degrees of unsolvability: infinite hierarchy

Rice's theorem: any non-trivial property of programs is undecidable.

Computability theory revealed that mathematics contains questions that no computer - no matter how powerful - could ever answer.

## Connections
→ [[turing_machines]]
→ [[complexity_theory]]
→ [[proof_theory]]
← [[logic_foundations]]

---
Level: L6
Date: 2025-06-20
Tags: #computability #decidability #limits