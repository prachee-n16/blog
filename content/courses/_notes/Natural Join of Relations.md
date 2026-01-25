Notation: $r \bowtie s$

Let $r$ and $s$ be relations on schemas $R$ and $S$, respectively. Then, $r \bowtie s$ is a relation on schema $R \cup S$ obtained as follows:
- Consider each pair of tuples $t_r$ from $r$ and $t_s$ from $s$.
- If $t_r$ and $t_s$ have the same value on each of the attributes in $R \cap S$, add a tuple $t$ to the result, where:
	- $t$ has the same value as $t_r$ for attributes in $R$.
	- $t$ has the same value as $t_s$ for attributes in $S$.

Natural join is commutative and associative.