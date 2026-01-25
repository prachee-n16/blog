The **closure of a set of functional dependencies** refers to all the functional dependencies that can be logically derived from a given set of dependencies.

> [!note] Mathematically,
> The closure of a set **F** of functional dependencies, denoted as **F+**, is the complete set of all functional dependencies that can be inferred from **F**.

For example, if we know that $A \to B$ and $B \to C$, we can infer $A \to C$. 

Therefore, it helps identify all possible functional dependencies, even those not explicitly stated, based on the original set of FDs.

**How do we get F+?**
- Start with the given set **F** of functional dependencies.
- Apply [[Armstrong’s Axioms]] to derive new dependencies
- Continue applying these rules until no new dependencies can be derived.

Similar to: [[Closure of Set of Attributes]], [[Canonical Cover]]