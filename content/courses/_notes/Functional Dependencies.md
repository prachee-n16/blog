Functional dependencies (FDs) are constraints between two sets of attributes in a relational database.
- Representation $X \to Y$ tells us that it means that if two rows of data have the same value for **X**, they must also have the same value for **Y**. In simple terms, knowing the value of **X** will always tell you the value of **Y**. 

For example, in a relation where **dept_name → building, budget**, knowing the department name uniquely determines the building and budget.

>[!note] Keys? Nope. General!
>A superkey is a set of one or more attributes that can uniquely identify a row in a table. In other words, if **K** is a superkey for a relation schema **R**, it means that **K $\to$ R**, where **K** determines all attributes of **R**.
>
> Functional dependencies are broader than keys. They allow us to express constraints between attributes that may not be related to unique identification. 
> 
> For example, in the table **inst_dept** with attributes like **ID**, **name**, **salary**, **dept_name**, **building**, and **budget**, we can have FDs such as **dept_name → building** and **ID → building**. These mean that knowing the department name or ID allows us to uniquely determine the building.
> 
> For example, **dept_name → salary** makes no sense but **ID → salary** will still work.

**Use**
1. Checking if Data is Valid: We use FD to check if table follows the rules. If set of FDs applies to a table and data satisfies all of them, data is "legal" under those FDs.
2. Defining Constraints: FDs also define rules for how data should behave across the whole table. 

A functional dependency is trivial if it is satisfied by all instances of a relation.

Related: [[Closure of Functional Dependencies]]