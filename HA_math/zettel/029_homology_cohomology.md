# Homology and Cohomology - Algebraic Topology

## Core Insight
Homology detects holes algebraically - turning geometric intuition into computational algebra.

## Content
How many holes does a space have? This innocent question leads to one of mathematics' most powerful tools: using algebra to study topology.

Homology assigns to each space a sequence of abelian groups:
- H₀: connected components
- H₁: 1D holes (loops)
- H₂: 2D holes (voids)
- And so on...

The construction:
- Chains: formal sums of simplices
- Boundary: faces of simplices
- Cycles: chains with no boundary
- Boundaries: chains that bound something
- Homology = Cycles/Boundaries

Key insight: boundaries have no boundary (∂∂ = 0).

Examples:
- Sphere: H₂(S²) = ℤ (one 2D hole)
- Torus: H₁(T²) = ℤ² (two independent loops)
- Projective plane: H₁(ℝP²) = ℤ/2ℤ (torsion!)

Cohomology is dual:
- Functions on chains
- Cup product: multiplication
- More structure, same information
- Natural for manifolds

Applications everywhere:
- Persistent homology: data has shape
- Knot theory: invariants
- Manifold recognition
- Robotics: configuration spaces

Homology revealed that holes have algebraic structure - and algebra remembers topology.

## Connections
→ [[algebraic_topology]]
→ [[persistent_homology]]
→ [[K_theory]]
← [[topology_shape]]

---
Level: L7
Date: 2025-06-20
Tags: #homology #cohomology #algebraic_topology