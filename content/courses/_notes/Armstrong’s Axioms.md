**Armstrong's Axioms** are a set of inference rules used to derive all possible functional dependencies from a given set. They are **sound** (only produce correct results) and **complete** (allow the derivation of all possible functional dependencies).

The three basic axioms:
1. **Reflexivity**:
	- If **Y** is a subset of **X**, then **X → Y** holds.
2. **Augmentation**:
	- If **X → Y** holds, then **XZ → YZ** also holds for any set of attributes **Z**.
3. **Transitivity**:
	- If **X → Y** and **Y → Z**, then **X → Z** holds.

We can use these axioms to infer additional rules:
1. **Union**:
    - If **X → Y** holds and **X → Z** holds, then **X → YZ** (the combination of **Y** and **Z**) also holds.
2. **Decomposition**:
    - If **X → YZ** holds, then both **X → Y** and **X → Z** hold separately.
3. **Pseudotransitivity**:
    - If **X → Y** holds and **YZ → Z** holds, then **XZ → Z** also holds.
