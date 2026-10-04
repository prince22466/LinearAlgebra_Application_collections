# General LA is for quick mental model when seeing some matrix;  
things like,   
what leads to what, what is the practical usage,   
what it implies in theory and numerical implementation,  
how it is connected to large scale optimization, etc

____________________________________________________________________________________

## Independent p ⇔ Independent Ap
Let p₁, p₂, p₃ ∈ ℝ³ be linearly independent vectors, aka c_1 p_1 + c2p2 + c3p3 =0, where c1=c2=c3=0.  

Assume A ∈ ℝ³ˣ³ is invertible.

Claim:
If { p₁, p₂, p₃ } is linearly independent, then
  c1 A p_1 + c2 A p2 + c3 A p3
= A (c1 p_1 + c2 p2 + c3 p3)
= 0

thus,
{ A p₁, A p₂, A p₃ } is also linearly independent if A is invertible. And vice versa.

________________________________________________________________________________________________
## orthogonal vectors => Independent vectors, but not in reverse

________________________________________________________________________________________________
## Determinant vs Condition Number
Determinant (A): The product of all eigenvalues (v1, v2, .....). It tells you the total -dimensional volume.

Condition Number (A): The ratio of the largest to smallest eigenvalues (vmax, vmin). It tells you how "stretched" or "squashed" the matrix is in a specific direction. The larger the Condition Number, the closer the matrix is to Singularity.
