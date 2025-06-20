# Matrices as Transformations

## Core Insight
Matrices are functions in disguise - they transform space by stretching, rotating, and reflecting.

## Content
A matrix looks like a grid of numbers, but it's really a machine that eats vectors and spits out new vectors. This perspective changes everything.

The matrix [[2,0],[0,2]] doubles all vectors. 
The matrix [[0,-1],[1,0]] rotates 90° counterclockwise.
The matrix [[1,0],[0,0]] projects onto x-axis.

Matrix multiplication isn't arbitrary - it's function composition:
- Apply transformation A, then B
- The result BA is their composition
- Order matters: BA ≠ AB (usually)

Key insights:
- Columns show where basis vectors go
- Determinant measures volume scaling
- Eigenvalues reveal invariant scaling
- Inverse undoes the transformation

Matrices appear everywhere:
- Computer graphics: rotating 3D models
- Quantum mechanics: state evolution
- Machine learning: weight layers
- Differential equations: systems of equations

Special matrices encode special transformations:
- Orthogonal: pure rotation
- Symmetric: nice eigenvalues
- Positive definite: bowl-shaped
- Nilpotent: eventually zero

The abstraction goes further:
- Tensors: multilinear transformations
- Operators: infinite-dimensional matrices
- Categories: transformations between structures

Matrices revealed that linear transformations are the atoms of geometry.

## Connections
→ [[linear_transformations]]
→ [[eigenvalues_eigenvectors]]
→ [[tensor_analysis]]
← [[vectors_spaces]]

---
Level: L4
Date: 2025-06-20
Tags: #matrices #transformations #linear_algebra