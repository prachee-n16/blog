---
title: Parse Trees
---

A parse tree represents visually the structure of program according to it's grammar. Each node represents a terminal or non-terminal symbol and relationships represent the production rules of the grammar. (See: [[backusNaurForm|Backus Naur Form]])

```
assignment_statement
     |
     v
variable_name = expression ;
      |           |        |
      v           v        v
      x           +        ;
                 / \
                5   2
```


