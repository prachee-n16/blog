Combinatorial analysis is the _mathematical theory of counting_.

**Basic Principle of Counting**
Number of ways to perform "several" procedures in succession

- If we perform $r$ procedures one after another, and for the $i^{th}$ procedure having $n_i$ possible ways after $i-1$ procedures are done, then $r$ procedures can be performed in $n_1n_2...n_r$ ways

Example:
Suppose you are choosing an outfit, with 3 shirts, 4 pants, and 2 pairs of shoes to choose from. The total number of possible outfits is $3×4×2=24$.

**Permutations**

1. Number of ways to order $n$ distinct elements: $n!$
   Example:
   -If $n=3$ and the objects are ${A,B,C}$, the possible arrangements are: $ABC,ACB,BAC,BCA,CAB,CBA$. In total, there are $3!=6$ arrangements
2. Number of ways to order $n$ elements which may not be distinct: $\frac{n!}{n_1!n_2!...n_r!}$
   - If some elements are repeated, the number of distinct arrangements decreases because swapping repeated elements does not create new unique arrangements.
3. Number of ways to select $r$ elements from $n$ elements: $P_r^n = \frac{n!}{(n-r)!}$

**Combinations**
Number of ways to select $r$ elements from $n$ distinct elements (order is not important): $C_r^n = \frac{n!}{r!(n-r)!}$

_Properties:_

- Note that: ${n}\choose{0}$ = ${n}\choose{n}$ = 1 and $n\choose{i}$ = 0 for $i < 0$ and for $i > n$
- $n\choose{r}$ = $n-1\choose{r-1}$ + $n-1\choose{r}$ where $1 \leq r \leq n$
- $n\choose{r}$ = $n\choose{n-r}$

**Binomial Theorem**
Way to expand powers of binomials using combinations:
{% raw %}
$(X+Y)^n = \sum^n_{k=0} {{n}\choose{k}} X_k Y_{n-k}$
{% endraw %}
**Multinomial Theorem**
This generalizes the Binomial Theorem to more than two variables. It is as follows:
$(x_1 + x_2 + ... + x_r)^n = \sum {n\choose{n_1, n_2, ..., n_r}} x_1^{n_1} x_2^{n_2} ... x_r^{n_r}$

where $n_1 + n_2 + ... + n_r = n$ and
${n\choose{n_1, n_2, ..., n_r}} = \frac{n!}{n_1!n_2!...n_r!}$

and the summation is over all possible sets of integers.

**Number of Integer Solutions of Equations**

- For positive integer solutions, there are ${{n-1}\choose{r-1}}$ distinct positive integer-valued vectors $x_1, x_2, ..., x_r$ satisfying: $x_1 + x_2 + ... + x_r = n$ as $x_i > 0, i = 1, ..., r$
- For non-negative integer solutions, there are ${{n+r-1}\choose{r-1}}$ distinct positive integer-valued vectors $x_1, x_2, ..., x_r$ satisfying: $x_1 + x_2 + ... + x_r = n$ as $x_i > 0, i = 1, ..., r$
