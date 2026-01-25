**Sample Space and Events**
- Experiment - procedure which results in an outcome; outcome depends on conditions under which experiment is performed
	- Deterministic - observed result is not subject to "chance" or randomness. If we repeat the experiment under the same conditions, we get the same result again.
	- Random - observed result is subject to "chance". If we repeat the experiment, the results change.
- Statistical Regularity - If a random experiment is repeated for a large number of times, and the fraction of times E occurs tends to some limit

- Sample Space - For any random experiment, define sample space S to be set of all possible outcomes of the experiment
- Elementary event - Single element of S corresponding to an outcome of the experiment
- Event - An event is any subset of S (collection of outcomes)

**Set Operations**
- Union of events: The union of events $E_1, E_2, ... E_n$ is when at least one of the event in the set of events occurs
- Intersection of events: The intersection of events $E_1, E_2, ... E_n$ is when all events in the set of events occurs
- Complement of events: Consider an event $E$; complement of E is the event that E does not occur. 
	- Properties: $EE^c = \emptyset$ and $E \cup E^c = S$      
- Partitioning of Sample Space: The events $F_1, F_2, ..., F_n$ form a partition S if they are disjoint and their union is S. 
	- $\bigcup_{i=1}^n E_i = S$ 
	- $E_i \cap E_j = \emptyset, \quad \text{for } i \ne j$ 

**Some Properties of Union and Intersection**
- Commutative Laws: $E \cup F = F \cup E$ and $EF = FE$
- Associative Laws: $(E \cup F) \cup G = E \cup (F \cup G)$ and $(EF)G = E(FG)$
- Distributive Laws: $(E \cup F)G = EG \cup FG$ and $(EF)\cup G = (E \cup G)(F \cup G)$

More importantly,
- **DeMorgan's Law**: $(A \cup B)^c = A^c \cap B^c$ or $(A \cap B)^c = A^c \cup B^c$
- **Law of Complements**: $E = EF^c \cup EF$ 
- **Inclusion-Exclusion Principle:**
$$P(E_1 \cup E_2 \cup E_3) = P(E_1) + P(E_2) + P(E_3) - P(E_1 E_2) - P(E_1 E_3) - P(E_2 E_3) + P(E_1 E_2 E_3)$$

Note that:
- $E\emptyset = \emptyset$ 
- $ES = E$
- $E \cup \emptyset = E$
- $E \cup S = S$

**Axioms of Probability**
- The probability of the event E is defined as $P(E) = \lim_{n\to\infty}\frac{n(E)}{n}$ and satisfies the following axioms:
	- $0 \leq P(E) \leq 1$ 
	- $P(S) = 1$
	- If $E_1, E_2...$ are disjoint events i.e. the intersection of any event returns the null set, then $P\left( \bigcup_{i=1}^{\infty} E_i \right) = \sum_{i=1}^{\infty} P(E_i)$

The axioms provides some simple propositions:
- $( P(E^c) = 1 - P(E)$
- If $E \subset F$, then $P(E) \leq P(F)$ 
- $P(E \cup F) = P(E) + P(F) - P(EF)$

For a Sample Space having N equally likely outcomes, probability of any event E is: $P(E) = \frac{\text{number of points in E}}{\text{number of points in S}}$
