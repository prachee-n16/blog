Conditional Probability: Consider two events $E$ and $F$ which depend on another. The conditional probability of E given F is defined as $P(E|F) = \frac{P(EF)}{P(F)} \text{ if } P(F) \neq 0$ 

Multiplication Rule: $P(E_1 E_2 E_3 \cdots E_n) = P(E_1) P(E_2 \mid E_1) P(E_3 \mid E_1 E_2) \cdots P(E_n \mid E_1 E_2 \cdots E_{n-1})$
- This rule tells us the probability of multiple events happening together is the product of the probability of the first event and the conditional probabilities of each subsequent event, given the previous events

Bayes Formula: calculates the total probability of event E by considering two cases (E occurring whether or not F occurs)
- $P(E \mid F) P(F) + P(E \mid F^c) [1 - P(F)]$ 

For multiple hypotheses, we get the **Law of total probability**:
$P(F_j \mid E) = \frac{P(E F_j)}{P(E)} = \frac{P(E \mid F_j) P(F_j)}{\sum_{i=1}^{n} P(E \mid F_i) P(F_i)}$

Odds Ratio: The odds ratio of an event $A$ is the ratio of the probability of $A$ happening to the probability of $A$ not happening. $$Odds(A) = \frac{P(A)}{P(A^c)} = \frac{P(A)}{1-P(A)}$$

*What happens if new "evidence" is introduced?* Consider a hypothesis $H$, which has a probability $P(H)$. When new evidence $E$ is introduced, we update the probability of $H$ given $E$. 
- The probability that H is true given the evidence E: $P(H \mid E) = \frac{P(E \mid H) P(H)}{P(E)}$
- The probability that H is false given the evidence E: $P(H^c \mid E) = \frac{P(E \mid H^c) P(H^c)}{P(E)}$

This updates the odd ratio to:
$\frac{P(H \mid E)}{P(H^c \mid E)} = \frac{P(H)}{P(H^c)} \cdot \frac{P(E \mid H)}{P(E \mid H^c)}$

**Axioms of Conditional Probability**
- $0 \leq P(E|F) \leq 1$ 
- $P(S|F)=1$
- If the events are disjoint, then the conditional probability of their union is the sum of their individual conditional probabilities.
