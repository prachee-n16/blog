The physical manifestation of relations is tables with rows and columns.
- Rows: Represent entities or even relationships
- Columns: Attributes
	- the set of allowed values for each attribute is domain of the attribute
		- i.e. the type of data allowed in the column
	- Attribute values have to be **atomic** (i.e. stores one data, not a set of values)
		- Dates are considered to be atomic, even if they have divisible components (month, year etc)
	- Special value NULL is a member of every domain; represents either missing or unknown data
		- This can complicate queries later so be wary!

##### Relation Schema and Instance
Let $A_1, A_2, ..., A_n$ denotes attributes.
Let $D_1, D_2, ..., D_n$ denotes domains.

Let $R(A_1, A_2, ..., A_n)$ denote a relation schema.
- e.g. in more human-readable form: `instructor (ID, name, dept_name, salary)`

A relation r conforming to schema R, denoted as r(R), is a subset of $D_1 \times D_2 \times ... \times D_n$
- This means table r is structured according to specification laid out in schema R. 
- The set $D_1 \times D_2 \times ... \times D_n$ represents all combination of values that could appear in the row.
