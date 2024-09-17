---
title: Syntax of Propositional Logic
---
*Syntax in regard to [[firstOrderLogic|First-order Logic]]*

To solve the ambiguity we can come across with a lack of parentheses in propositional statements, we define everything as trees.
- A leaf is labelled by an atomic proposition (can't be broken down further really) 
- Some nodes will have an operator with it. The ¬ symbol will only ever have one child but, $\land$ will have two children which are both formulas
- The set F of all formulas is the smallest set that satisfies the above properties
The last point prevents propositions with infinite depth or infinite trees (think about negating a atomic proposition again and again)

The term formula will also be applied to appropriate strings with the understand that it refers to the underlying tree.

Since it's difficult to always work with trees, can we convert them back to string state. Note, it's an in-order traversal of a tree

**Input: A formula A of propositional logic.
Ouput: A string representation of A**
Given A, we build a string by calling InOrder(A) where InOrder is defined as follows:
InOrder(F)
```
If F is a leaf
	write its label
	return
```
This is our base case, simplest thing that can happen. What if it is not a leaf?
```
Let F1 and F2 be the left and right sub-trees of F
InOrder(F1)
write the label of the root of F
InOrder(F2)
```
If the root of F is labelled by ¬, the left subtree is considered to be an empty tree and we skip the step InOrder(F1)

Example 1: The important thing to note is that we go from left->node->right according to this algorithm. Also, when encountering negation, the left node is null. 
The prints of both trees in lecture example leads to ambiguities, so we need to add parentheses into our algorithm. 
```
Write Left Parentheses '('
Let F1 and F2 be the left and right sub-trees of F
InOrder(F1)
write the label of the root of F
InOrder(F2)
Write Right Parentheses ')'
```

Having more parenthesis than "needed" make it harder to read expressions. Here, are order of operations and associativity rules.
1. () - Not actually an operator but the first thing we will do
2. ¬ - negation, it's the next thing we do in maths
3. $\land$ and before OR
4. $\lor$ 
5. $\implies$ 
6. $\iff$ $\oplus$
Note 3, 4, 6 are all associative but the rest are usually not. **What is this up/down symbol?**

Now, let's look at the Polish Notation, which is really just pre-order traversal.
```
Given A, to build a string by calling PreOrder(A) where PreOrder is defined as follows:
PreOrder(F):
	If F is a leaf,
		write its label
		return
	Write the label of the root of F
	Let F1 and F2 be the left and right sub-trees of F
	PreOrder(F1)
	PreOrder(F2)
If the root is labelled by null, left is considered to be the empty tree.
```

Reverse Polish Notation: Reverse the order of a string gives us a new string representation of the formula.
We define the following operations:
- push p - push onto the stack the tree consisting of a leaf labelled by p
- Op (for a standard operation) - pop the two subtrees from top, then push onto the stack the tree whose root is labelled Op

An unambiguous string representation of a formula will also be referred to as the formula.
