See [[Data Definition Language]]

> [!note] Multiset Relations
> Multiset relations in SQL allow for duplicate tuples, unlike set-based relations where each tuple must be unique. Multiset relational algebra extends standard relational algebra by incorporating multiplicity. Key operations like **selection (σ)**, **projection (π)**, and **Cartesian product (×)** preserve or adjust the multiplicity of tuples based on the operation.

**Basic Query Structure**
> SELECT $A_1, A_2, ..., A_n$
> FROM $r_1, r_2, ..., r_m$
> WHERE $P$

In [[Relational Models|relational algebra]], $\Pi_{A_1, A_2, ..., A_n} (\sigma_P(r_1 \times r_2 \times ... \times r_m))$   
- [[Project Operator]] relates to SELECT clause
	- keyword distinct eliminates duplicates
	- keyword all keeps duplicates
	- asterisk i.e. SELECT * denotes all attributes
- [[Select Operator]] relates to WHERE clause
	- Comparison results can be combined using the logical connectives and, or, and not
- [[Cartesian Product of Relations]] relates to FROM clause
	- lists the relations involved in the query; 

More on: [[SQL Commands]]