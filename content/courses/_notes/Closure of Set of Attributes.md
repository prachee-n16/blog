The closure of a set of attributes **α**, denoted as **α+**, is the complete set of attributes that can be functionally determined by **α** based on a given set of [[Functional Dependencies]] **F**.

Why? Well, we can determine which attributes are implied by a set of attributes. It also allows us to check if a set of attributes is a **superkey** or test whether a particular functional dependency holds in a relation.

**Example**:
If the set of functional dependencies **F** contains the following:
- **A → B**, **B → C**, **C → D**, then:
    - The closure of **A** (denoted **A+**) would be **{A, B, C, D}** because **A** can determine **B**, **B** can determine **C**, and **C** can determine **D**.