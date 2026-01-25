---
title: Parser
---
A parser turns the list of tokens generated from the [[Lexer]] into a tree of nodes, called an Abstract Syntax Tree (AST). It adds structure to ordered list of tokens, takes parenthesis and order of operations into account. 

The parser reads the code and checks if it follows the rules defined in the [[Backus-Naur Form|BNF]]. If the code is valid, the parser builds a **[[Parse Trees|parse tree]]**.
