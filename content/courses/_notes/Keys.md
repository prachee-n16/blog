Let $R$ be a relation schema and let $K \in R$   i.e. K is a subset of R's attributes or K is a "column" in the table.

**Superkey**: A set of attributes K is a superkey for a relation R if the values of K can uniquely identify each tuple in every possible instance of the relation based on the schema R.
- `ID` or `ID, name` are examples of possible superkeys.

**Candidate Key**: Superkey K is a candidate key if K is "minimal"
- `ID` is an example of a candidate key
- **Primary Key** is a candidate key

**Foreign Key** constraint: an attribute value in one relation that must appear in another relation
- The child table or "referencing relation" has the foreign key
- The parent table of "referenced relation" has the key.

