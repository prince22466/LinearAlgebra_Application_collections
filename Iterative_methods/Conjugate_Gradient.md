# Conjugate Gradient (CG) Method — Numerical Iterative Methods

## Problem Setting

We consider solving a linear system

A x = b

where:
- A ∈ ℝⁿˣⁿ is **symmetric positive definite (SPD)**,
- b ∈ ℝⁿ,
- x ∈ ℝⁿ is unknown.

find x (approximate)

No one wants to do inverse,
No one wants to A decomposition (e.g., Cholesky decomposition)
No one wants to do Gussian Elimination.

Iterative methods such as **Conjugate Gradient (CG)** exploit the SPD structure of A to achieve fast convergence with low memory usage.  

The idea is to take away a component p from r in each iteration, here p is a vector, r is residual (r = b - A x). And finally iteration stops when |r²| become 0 or reach certain criterion. 
And keep components p A-conjugate (A-orthogonal, aka uncorrelated with each other under A).  
And keep residuals r orthogonal with components p of previous iterations.  
---

## Interpretation as an Optimization Problem

Solving A x = b is equivalent to minimizing the quadratic function

f(x) = ½ xᵀ A x − bᵀ x

Properties:
- f is strictly convex because A is SPD,
- The unique minimizer x* satisfies ∇f(x*) = 0 ⇔ A x* = b.

---

## Residual and Gradient

Define:
- Residual: rₖ = b − A xₖ
- Gradient: ∇f(xₖ) = −rₖ

Thus, the residual is the **negative gradient** of the objective function.

---

## Key Idea of Conjugate Gradient

CG constructs a sequence of search directions {p₀, p₁, …} such that:

pᵢᵀ A pⱼ = 0   for i ≠ j

These directions are **A-conjugate (A-orthogonal)**.

This is stronger than standard orthogonality and is crucial for finite-step convergence.

---

## Algorithm Outline

### Initialization
Choose an initial guess x₀ (often x₀ = 0):

- r₀ = b − A x₀
- p₀ = r₀

---

### Iteration (k = 0, 1, 2, …)

1. **Step size**
   
   αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ)

2. **Update solution**
   
   xₖ₊₁ = xₖ + αₖ pₖ

3. **Update residual**
   
   rₖ₊₁ = rₖ − αₖ A pₖ

4. **Direction update coefficient**
   
   βₖ = (rₖ₊₁ᵀ rₖ₊₁) / (rₖᵀ rₖ)

5. **New search direction**
   
   pₖ₊₁ = rₖ₊₁ + βₖ pₖ

---

## Orthogonality Properties

- Residuals are mutually orthogonal:
  
  rᵢᵀ rⱼ = 0  for i ≠ j

- Search directions are A-conjugate:
  
  pᵢᵀ A pⱼ = 0  for i ≠ j

These properties ensure that each iteration eliminates error components in independent eigenspaces of A.

---

## Krylov Subspace View

At iteration k:

xₖ ∈ x₀ + 𝒦ₖ(A, r₀)

where the Krylov subspace is defined as:

𝒦ₖ(A, r₀) = span{ r₀, A r₀, A² r₀, …, A⁽ᵏ⁻¹⁾ r₀ }

CG computes the **best approximation** to x* over this subspace in the A-norm.

---

## Convergence Properties

- CG converges in at most n steps in exact arithmetic.
- In practice, convergence depends on the eigenvalue distribution of A.
- Well-clustered eigenvalues lead to fast convergence.

---

## Why CG is Efficient

- No matrix factorization required,
- Only matrix–vector products A pₖ,
- O(n) memory usage,
- Exploits symmetry and positive definiteness.

---

## Summary

The Conjugate Gradient method:
- Is designed specifically for SPD systems,
- Combines gradient descent with A-orthogonalization,
- Eliminates error components one eigendirection at a time,
- Achieves optimal convergence within Krylov subspaces.


## FAQ
