It's used to describe syntax of formal languages and provides a way to define the set of valid grammatical structures allowed in a language.

The key concepts are:
- Symbols, the building blocks of a language can be terminal or non-terminal symbols
	- Terminal symbols represents basic elements like keywords (e.g. "if", "for"), operators, punctuation marks or literals
	- **Non-terminal symbols:** Represent categories or groups of elements, such as variables or numbers. They may also be called simply **syntactic variables**.
- Production Rules define how non-terminal symbols are expanded or replaced with other symbols

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Terminal_and_non-terminal_symbols_example.png/900px-Terminal_and_non-terminal_symbols_example.png)

For example, if we want to define "Assignment" as a production rule, this would look like:
```
<assignment> ::= <variable_name> = <expression> ;
```

Note, this describes syntax but not the semantics of code. Here's how to write different rules in this notation:

| Symbol | Meaning                                                  |
| ------ | -------------------------------------------------------- |
| ""     | Encloses a terminal symbol                               |
| <>     | Encloses a non-terminal symbol                           |
| ()     | Indicates a group of valid options                       |
| +      | Specifies one or more of the previous element            |
| *      | Specifies zero or more of the previous element           |
| ?      | Specifies zero or one occurrence of the previous element |
| \|     | OR from these options                                    |
| [x-z]  | Indicates letter or digit intervals                      |


