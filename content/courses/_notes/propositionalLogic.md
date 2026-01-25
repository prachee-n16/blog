---
title: Propositional Logic
---
**Syntax**
- $Op$ is a set of logical operators, such as {$\neg$, $\land$, $\lor$, ...}
- $\Sigma$ is a set of symbols
	- Elements of set $\Sigma$ are called propositional variables
- {t, f} is the set of truth values i.e. true/false

The set of formulas is:
- {t, f} and all elements of $\Sigma$  are **atomic formulas** i.e. no subformulas.
- If A and B are formulas, they can be coupled with elements of $Op$ to make new formulas 
	e.g. A $\land$ B

| Symbol     | Meaning   |
|-----------|------------------|
| t         | True                            |
| f         | False            |
| $\neg$    | Not              |
| $\land$   | And              |
| $\lor$    | Or               |
| $\implies$| Implies          |
| $\iff$    | If and only if   |

**Semantics**
Every propositional variable can be either true or false, so formula with n propositional variable will have $2^n$ intepretations. All intepretations can be represented in a truth table. 
- Two formulas are *semantically equivalent* if they have the same truth table, denoted by F $\equiv$ G

If a formula is true for one interpretation, it is *satisfiable*
If a formula is true for all interpretations, it is *logically valid* or tautologies.
If a formula is not true for any interpretation, it is *unsatisfiable*

**Proof Systems**
In AI, we take what we already know and derive new information. Mathematically, we want to show formula Q follows from a formula KB (knowledge base).
- Entailment: A formula KB entails formula Q if every model of KB is also a model of Q.

