# General LA is for quick mental model when seeing some matrix;  
things like,   
what leads to what, what is the practical usage,   
what it implies in theory and numerical implementation,  
how it is connected to large scale optimization, etc

____________________________________________________________________________________
## Breakdown Representation of Ab, and AB matrix-vector, matrix-matrix multiplication

A = [A₁, A₂], b = [k, v]ᵀ

A₁, A₂ are vectors; k, v are scalers.

Ab = kA₁ + vA₂

A = [A₁, A₂], B = [B₁, B₂]

A₁, A₂, B₁, B₂ are vectos.

AB = [AB₁, AB₂]
____________________________________________________________________________________
## Linear dependency, Singularity, Determinant, Linear transformation

For matrix A with ℝⁿˣⁿ,

rows linear dependent  
⇔ singular  
⇔ det(A) = 0  
⇔ row rank(A) < n

rank = row number → non-singular, otherwise singular.

If matrix A is singular, for C = Ab with A is square and b as a vector, C can only occupy a lower-dimensional subspace because rank(A) < n(the linear transformation effect of A on b is to reduce the richness of b).

If A is non-singular, all possible values of C will make up the whole 2D plane.

det(AB) = det(A) · det(B)

⇒ det(A²) = (det(A))², and so on.

If A is singular,

det(AB) = 0

Row operations preserve singularity(or nonsingularity) characteristics of matrix.
____________________________________________________________________________________
## Independent p ⇔ Independent A p

Let p₁, p₂, p₃ ∈ ℝ³ be linearly independent vectors, aka

c₁p₁ + c₂p₂ + c₃p₃ = 0, only when c₁ = c₂ = c₃ = 0.

Assume A ∈ ℝ³ˣ³ is invertible.

Claim:

If p₁, p₂, p₃ is linearly independent, then

c₁Ap₁ + c₂Ap₂ + c₃Ap₃  
= A(c₁p₁ + c₂p₂ + c₃p₃)  
= 0

thus,

Ap₁, Ap₂, Ap₃ is also linearly independent if A is invertible. And vice versa.

________________________________________________________________________________________________
## Orthogonal vectors ⇒ Independent vectors, but not in reverse

Orthogonal means p₁ᵀp₂ = 0.

Independency means c₁p₁ + c₂p₂ + c₃p₃ = 0 only when c₁ = c₂ = c₃ = 0.

Given p₁ᵀp₂ = 0 (orthogonal), and c₁p₁ + c₂p₂ + c₃p₃ = 0,

c₁p₁ᵀp₁ + c₂p₁ᵀp₂ + c₃p₁ᵀp₃ = 0

⇒ c₁‖p₁‖² + c₂·0 + c₃·0 = 0

⇒ c₁ = 0

Same can be shown for c₂ and c₃, thus p₁, p₂, p₃ are independent.

the counter case for the reverse,
For example,
p₁ = [1, 0], p₂ = [1, 1]
are linearly independent, but
p₂ᵀp₁ = 1 ≠ 0,
so they are not orthogonal.
________________________________________________________________________________________________
## Determinant vs Condition Number
Determinant (A): The product of all eigenvalues (v1, v2, .....). It tells you the total -dimensional volume.

Condition Number (A): The ratio of the largest to smallest eigenvalues (vmax, vmin). It tells you how "stretched" or "squashed" the matrix is in a specific direction. The larger the Condition Number, the closer the matrix is to Singularity.
