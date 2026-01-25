A **canonical cover** is a simplified and minimal set of functional dependencies (FDs) that is equivalent to the original set of FDs in a relational database. The purpose of a canonical cover is to remove any redundancies while preserving the same functional relationships.

For example, if we have **A → B**, **B → C**, and **A → C**, the last dependency (**A → C**) is redundant because it can be derived from the first two using [[Armstrong’s Axioms|transitivity]] (i.e., **A → B** and **B → C** together imply **A → C**).



[[Extraneous Attributes]]