QUBO problem is defined by a matrix Q (upper triangular) and a vector of binary variables x. The mathematical form of a QUBO (Quadratic Unconstrained Binary Optimization) problem is given as $f(x) = \sum_i a_i x_i + \sum_{i<j} b_{ij} x_i x_j$ 
- $x \in {0, 1}$ or binary variable, $a_{ij}$ are linear coefficients, $b_{ij}$ are quadratic coefficients

Assume a QUBO matrix Q:
$$
Q = \begin{bmatrix}
1 & -2 \\
0 & 3
\end{bmatrix}
$$
This can be converted to the energy function:
$E(x) = Q_{11}x_1 + Q_{22}x_2 + Q_{12}x_1x_2$
$E(x) = x_1(1) + x_2(3) + x_1 x_2 (-2)$

So, a classical QUBO can be converted into a hamiltonian:
$H_{\text{problem}} = Q_{11} x_1 + Q_{22} x_2^2 + Q_{12} x_1 x_2$ and $H_{\text{problem}} = Q_{11} \hat{x}_1 + Q_{22} \hat{x}_2^2 + Q_{12} \hat{x}_1 \hat{x}_2$
