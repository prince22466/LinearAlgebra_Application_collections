# Conjugate Gradient (CG) — Numerical Iterative Methods

## Problem Setting

We consider solving a linear system

A x = b

where:
- A ∈ ℝⁿˣⁿ is **symmetric positive definite (SPD)**,
- b ∈ ℝⁿ,
- x ∈ ℝⁿ is unknown.

find x (approximate)

No one wants to inverse matrix,
No one wants to A decomposition (e.g., Cholesky decomposition)
No one wants to do Gussian Elimination (complicated).
Only doing matrix–vector products is much easier, if possible.

Iterative methods such as **Conjugate Gradient (CG)** exploit the SPD structure of A to achieve fast convergence with low memory usage.  

## Main idea
The idea is to take away a component p from r in each iteration, here p is a vector, r is residual (r = b - A x). And finally iteration stops when ‖r‖² (aka, rᵀr) become 0 or reach certain criterion.  
And keep components p A-conjugate (A-orthogonal, aka uncorrelated with each other under A).  
And keep residuals r orthogonal with components p of previous iterations.  

---
# Algo Outline
Define:
- Residual: rₖ = b − A xₖ, rₖ₊₁ = b − A xₖ₊₁, 
- x update formula: xₖ₊₁ = xₖ + αₖ pₖ
- p update formula: pₖ₊₁ = rₖ₊₁ + βₖ pₖ and p₀ = r₀

Given Residual formulas,  
rₖ₊₁ - rₖ = − A (xₖ₊₁ - xₖ)  
#### rₖ₊₁ = rₖ − A αₖ pₖ      <--- this is the iteration process to reduce residual  
with αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ), and βₖ = (rₖ₊₁ᵀ rₖ₊₁) / (rₖᵀ rₖ)

---
## Calculation Demo
[Visible link text](https://www.example.com)
---

## Key Idea of Conjugate Gradient

CG constructs a sequence of search directions {p₀, p₁, …} such that:

pᵢᵀ A pⱼ = 0   for i ≠ j

These directions are **A-conjugate (A-orthogonal)**.

This is stronger than standard orthogonality and is crucial for finite-step convergence.

---

## Orthogonality Properties in CG

- Residuals are orthogonal to previous components (explicit requirement):
  
  pᵢᵀ rⱼ = 0  for i < j
  
- Residuals are mutually orthogonal (implicit):
  
  rᵢᵀ rⱼ = 0  for i ≠ j

- Search directions are A-conjugate (implicit):
  
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
- αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ), and βₖ = (rₖ₊₁ᵀ rₖ₊₁) / (rₖᵀ rₖ), how these are derived ?  
  <details>
  <summary>Click to show</summary>
  for αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ),  
  it is from rₖ₊₁ ⟂ pₖ = 0 (r doesnt have components in previous iteration),  
  rₖ₊₁ = rₖ − αₖ A pₖ  
  pₖᵀ rₖ₊₁ = pₖᵀ rₖ − αₖ pₖᵀ A pₖ  
  0 = pₖᵀ rₖ − αₖ pₖᵀ A pₖ  
  αₖ = (pₖᵀ rₖ) / (pₖᵀ A pₖ)  

  because pₖ = rₖ + βₖ₋₁ pₖ₋₁, dot product with rₖ becomes, pₖᵀ rₖ = rₖᵀ rₖ + βₖ₋₁ pₖ₋₁ᵀ rₖ,  
  then pₖᵀ rₖ = rₖᵀ rₖ since pₖ₋₁ᵀ rₖ = 0.  
  Thus αₖ = (pₖᵀ rₖ) / (pₖᵀ A pₖ) = (rₖᵀ rₖ) / (pₖᵀ A pₖ)  

  for βₖ = (rₖ₊₁ᵀ rₖ₊₁) / (rₖᵀ rₖ),  
  it is from pₖ₊₁ ⟂ A pₖ = 0 (p is A-orthogonal or A-conjugate, aka, pᵢᵀ A pⱼ = 0  for i ≠ j),  
  pₖ₊₁ = rₖ₊₁ − βₖ pₖ  
  pₖᵀ A pₖ₊₁ = pₖᵀ A rₖ₊₁ − βₖ pₖᵀ A pₖ  
  0 = pₖᵀ A rₖ₊₁ − βₖ pₖᵀ A pₖ  
  βₖ = - (pₖᵀ A rₖ₊₁) / (pₖᵀ A pₖ)  <---- this is the conceptally correct one  

  since rₖ₊₁ ⟂ rₖ = 0,  
  with rₖ₊₁ = rₖ − A αₖ pₖ  
  rₖ₊₁ᵀ rₖ₊₁ = rₖ₊₁ᵀ rₖ - αₖ rₖ₊₁ᵀ A pₖ  
  rₖ₊₁ᵀ A pₖ = (rₖ₊₁ᵀ rₖ₊₁) / αₖ  
  then, βₖ = (rₖ₊₁ᵀ rₖ₊₁) / αₖ (pₖᵀ A pₖ), A is symmetric so rₖ₊₁ᵀ A pₖ == pₖᵀ A rₖ₊₁,  
  given the case above, αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ),  
  finally, βₖ = (rₖ₊₁ᵀ rₖ₊₁) / (rₖᵀ rₖ) <---- this is for computation, it only has vector multiplication  

- what does it mean, one vector r doesnt have component p ?
  <details>
  <summary>Click to show</summary>
  Let r and p be vectors, p ≠ 0. r can be decomposed into 2 components of p,
  
  r = (pᵀr / pᵀp) p + ( r − (pᵀr / pᵀp) ) p
  
  where:
  
  • (pᵀr / pᵀp) p is the component of r,   
  • r − (pᵀr / pᵀp) p is the component of r orthogonal to p

  for (pᵀr / pᵀp) p to be zero, pᵀr = 0 is required, and it means r doesnt have component of p.

- pᵢᵀ A pⱼ = 0  for i ≠ j, how this is dervied?  
  <details>
  <summary>Click to show</summary>
  it is from rₖ₊₁ ⟂ pₖ = 0,
    
  rₖ₊₁ = rₖ − αₖ A pₖ
  
  pₖ₋₁ᵀ rₖ₊₁ = pₖ₋₁ᵀ rₖ − αₖ pₖ₋₁ᵀ A pₖ
  
  0 = 0 − αₖ pₖ₋₁ᵀ A pₖ
  
  the equation holds with certainty, when pₖ₋₁ᵀ A pₖ = 0

- pₖ₊₁ = rₖ₊₁ + βₖ pₖ, why p is updated in this manner ?
  <details>
  <summary>Click to show</summary>
  intuitively, in the step to update pₖ₊₁, the available info is pₖ, pₖ₋₁, ...p₀, rₖ₊₁, rₖ, ...r₀

  the way to update pₖ₊₁ will be constrained to use the linear combination of these elements and their polynomials, such as pₖ, pₖ², pₖ₋₁², rₖ₊₁, rₖ²,    rₖ₋₁².

  amony which rₖ₊₁ + scaler* pₖ is the simplest one, and it works.

  This is the general form in iterative methods not just in CG.

- residuals are mutually orthogonal (aka, rᵢᵀ rⱼ = 0  for i ≠ j), how it this derived ?  
  <details>
  <summary>Click to show</summary>
  it is from pᵢᵀ rⱼ = 0,
    
  pₖ₋₁ᵀ rₖ = 0
  
  rₖᵀ pₖ₋₁ = 0
  
  rₖᵀ (rₖ₋₁ + βₖ₋₂ pₖ₋₂) = 0
  
  rₖᵀ rₖ₋₁ + βₖ₋₂ rₖᵀ pₖ₋₂ = 0
  
  rₖᵀ pₖ₋₂ = 0, then rₖᵀ rₖ₋₁ = 0

- How A as a SPD(symmetric positive definite) matrix affect the effectiveness of CG ?
  <details>
  <summary>Click to show</summary>
  if A is not symmetric, then pᵢᵀ A pⱼ != pⱼᵀ A pᵢ .
    
  And mostly importantly, if A is not SPD, pᵢᵀ A pᵢ will not garantee to be positive,

  then αₖ = (rₖᵀ rₖ) / (pₖᵀ A pₖ) cannot have consistent sign during iterations, which makes process of solution searching unstable.
 
- Why CG converges in at most n steps in exact arithmetic ?
