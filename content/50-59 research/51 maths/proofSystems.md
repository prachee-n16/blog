---
title: Introduction to Proof Systems
---
In ECE 108:
- Defined the [[propositionalLogicSyntax|syntax]] and semantics of our propositions. By semantics, we talk about the "meaning in logic" so e.g. implies
- We then defined a proof system to prove various propositions are tautologies (always true)
	- These proof systems are called semantic proofs (need to understand what this means)
- This term, we examine logic and deductive systems more formally.

Logic first developed from the precise use of language via rules called syllogisms.

==Syllogism==: an instance of a form of reasoning in which a conclusion is drawn (whether validly or not) from two given or assumed propositions (premises)
- Euclidean geometry: study of geometrical shapes and figures based on different axioms/theorems
	- Parallel lines can not cross
- Some non-euclidean geometry had parallel lines crossing, which lead to a re-examination of truth
Truth of a statement depends on the axioms and inference rules included. 
- The sum of the angles on a triangle is 180º holds true if **we assume parallel lines don't cross.**

A system of logic should have the following properties:
1. Consistency: Logical system is consistent if it is impossible to prove both a formula and its negation (i.e. Proof by Contradiction is based on a consistent logical system)
2. Independence: Axioms are independent if no axiom can be proved from others
3. Soundness: All theorems can be proved in the logical system are true
4. Completeness: All true statements can be proved in a logical system
Related: [Godel's Incompleteness Theorem](https://prachee.me/notes/Areas/Math/G%C3%B6dels-Incompleteness-Theorem#:~:text=incom)

SAT Problem and Computational Complexity
- determining if all elements of a set of propositional-logic formulas can be SATisfied at the same time. i.e. can all be true

If SAT problem can be solved in poly. time, then you can solve a LARGE number of hard problems quickly. [NP-complete problems](https://en.wikipedia.org/wiki/List_of_NP-complete_problems)

Non-deterministic: There's some randomness to the problem, and solution can be checked in poly. time
NP-complete: Problems that all NP problems can be transformed to in poly.time
Missing in above problem: [NP-Hard](https://mathworld.wolfram.com/NP-HardProblem.html#:~:text=A%20problem%20is%20NP%2Dhard,%2C%20in%20fact%2C%20be%20harder.)

Formal verification helps in cache coherency, 5G networks and cloud computing services.
![](https://upload.wikimedia.org/wikipedia/commons/a/a1/Cache_Coherency_Generic.png)

Modal Logic - quantify truth of propositional statements in a dynamic environment.