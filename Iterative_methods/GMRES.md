# GMRES (Generalized Minimal Residual) — Numerical Iterative Methods

---

## Problem Setting

We want to solve the linear system

A x = b

where

* A ∈ ℝⁿˣⁿ is **large**, possibly **non‑SPD**
* b ∈ ℝⁿ
* x ∈ ℝⁿ is unknown
* goal: find x approximately

For large systems:
* matrix inverse, LU / QR / Cholesky factorization, Gaussian elimination are expensive
* Matrix–vector products (A·v) with iteration are cheap and easier to do in computer.

When A is not SPD, Conjugate Gradient cannot be used.
**GMRES works for general matrices.**

---

## Main idea

Instead of find the x, we
* find xₖ that **makes the residual norm small enough** by iteration

And then How?
* x(solution) is ℝⁿ, then x = Vₙ Yₙ, Vₙ is a span of ℝⁿ, each vectos in Vₙ are orthognormal to each other , Yₙ is a vector of n scalers.
* x can be represented as a linear combination of orthognormal vectors(v₁, v₂, ⋯, vₙ) in Vₙ , x = y₁v₁ + y₂v₂ + ⋯ + yₙvₙ.
* given x₀(initial guess, usually zero), x = x₀ + y₁v₁ + y₂v₂ + ⋯ + yₙvₙ. It seems starting from x₀ and then adding orthognormal vectors, we can finally reach x from x₀.
* then comes the iteration formular xₖ = x₀ + Vₖ Yₖ, where Vₖ has k orthognormal vectors, Yₖ is a vector k scalers.
* hence we can represent rₖ = b − A xₖ => rₖ = r₀ − A Vₖ yₖ , r₀ = b - A x₀.
* with Arnold Decomposition, rₖ = r₀ − Vₖ₊₁ Hₖ₊₁,ₖ yₖ, A is gone, Hₖ₊₁,ₖ is hessenberg matrix.
* if we set up v₁ = r₀ / β , β = ∥r₀∥, then v₁ = e₁ Vₖ₊₁ , e₁ is [1,0,0,0...] .
* then rₖ = β e₁ Vₖ₊₁ − Vₖ₊₁ Hₖ₊₁,ₖ yₖ =  Vₖ₊₁ (β e₁ - Hₖ₊₁,ₖ yₖ) , further, ∥rₖ∥ = ∥β e₁ - Hₖ₊₁,ₖ yₖ∥, because ∥Vₖ₊₁∥ =1, 
* so Now, we need to find k(much smaller than n) and xₖ, that make ∥rₖ∥=  small enough

Each iteration:

1. add one new direction
2. project A to a small matrix
3. solve a tiny least‑squares problem
4. update x
5. residual decreases

So:

large problem → small least squares

---
## Algo Outline
## Parameterization of the iterate

xₖ = x₀ + Vₖ yₖ

where

* Vₖ = [v₁, …, vₖ] with orthonormal columns
* yₖ ∈ ℝᵏ (small coefficient vector)

---

## Residual

rₖ = b − A xₖ

Substitute:

rₖ = b − A(x₀ + Vₖ yₖ)
rₖ = r₀ − A Vₖ yₖ

where

r₀ = b − A x₀

---

## Arnoldi decomposition

Instead of computing A Vₖ directly, use Arnoldi:

A Vₖ = Vₖ₊₁ Hₖ₊₁,ₖ

where

* Vₖ₊₁ orthonormal
* Hₖ₊₁,ₖ small (k+1)×k upper Hessenberg matrix

This projects

big matrix A → small matrix H

---

## Substitute back

Let

r₀ = β v₁,   β = ∥r₀∥

Then

rₖ = Vₖ₊₁ (β e₁ − Hₖ₊₁,ₖ yₖ)

Because Vₖ₊₁ is orthonormal:

∥rₖ∥ = ∥β e₁ − Hₖ₊₁,ₖ yₖ∥

---

## Least‑squares problem

Solve

yₖ = argminᵧ ∥β e₁ − Hₖ₊₁,ₖ y∥²

This is a **small least‑squares problem**.

Usually solved by:

* QR decomposition
* Givens rotations (incremental and efficient)

---

## Update solution

xₖ = x₀ + Vₖ yₖ

---

# Algorithm Outline

## Initialization

r₀ = b − A x₀
β = ∥r₀∥
v₁ = r₀ / β

---

## Iteration (k = 1, 2, …)

### Step 1 — Arnoldi expansion

w = A vₖ

For j = 1 … k

hⱼₖ = vⱼᵀ w
w = w − hⱼₖ vⱼ

hₖ₊₁,ₖ = ∥w∥
vₖ₊₁ = w / hₖ₊₁,ₖ

---

### Step 2 — Solve small least squares

min ∥β e₁ − Hₖ₊₁,ₖ y∥

---

### Step 3 — Update iterate

xₖ = x₀ + Vₖ yₖ

---

### Step 4 — Stop condition

Stop when

∥rₖ∥ ≤ tolerance

---

# Key properties

• works for non‑symmetric matrices
• only requires matrix–vector products
• explicitly minimizes residual norm
• memory grows with k (store all vᵢ)
• commonly restarted → GMRES(m)

---

# Geometric interpretation

GMRES chooses

xₖ ∈ x₀ + span{v₁,…,vₖ}

such that

∥b − A xₖ∥ is minimal

So:

CG → minimize energy (A‑norm)
GMRES → minimize residual (2‑norm)

---

# Cost per iteration

• 1 matrix–vector multiply
• k inner products
• k vector updates
• small least‑squares solve

---

# One‑line summary

GMRES builds an orthonormal basis, projects A to a small Hessenberg matrix, solves a small least‑squares problem, and updates x to minimize the residual.
