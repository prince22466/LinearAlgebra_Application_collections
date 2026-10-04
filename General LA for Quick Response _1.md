# General LA is for quick mental model when seeing some matrix;  
things like,   
what leads to what, what is the practical usage,   
what it implies in theory and numerical implementation,  
how it is connected to large scale optimization, etc

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
## orthogonal vectors => Independent vectors, but not in reverse
orthogonal means p1Tp2 = 0, independency means c1p1 + c2p2 + c3p3 = 0 only with c1=c2=c3=0.
given p1Tp2 = 0, and c1p1 + c2p2 + c3p3 = 0,
c1 p1Tp1 + c2 p1Tp2 + c3 p1Tp3 = 0
=> c1 + c2 0 + c3 0 = 0
=> c1 = 0
same can be shown for c2 and c3, thus p1, p2 ,p3 are independent
________________________________________________________________________________________________
## Determinant vs Condition Number
Determinant (A): The product of all eigenvalues (v1, v2, .....). It tells you the total -dimensional volume.

Condition Number (A): The ratio of the largest to smallest eigenvalues (vmax, vmin). It tells you how "stretched" or "squashed" the matrix is in a specific direction. The larger the Condition Number, the closer the matrix is to Singularity.
