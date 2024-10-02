
- Considered as the first step towards building today's neural networks
	- It's not the first NN; but also served as foundation of FSM and Regex.
- **Perceptron learning rule**: Start with random weights (or zero)
	- This is supervised learning where we apply inputs with a known output
		- If output is wrong, change the weights. **How do we know what to change the outputs to?**

Example: 
$$
y = 
\begin{cases} 1 \text{ if } \sum_i x_i\omega_i > \theta \\
0 \text{ otherwise}
\end{cases}
$$
Given the inputs:

| x   | w   | Decision  | Why?                                                                                                                  |
| --- | --- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| 1   | 0.2 | increase; | We want to be above base amount of $\theta$. Since input x is positive, weight needs to increase.                     |
| 0   | 0.3 | stay;     | We want to be above base amount of $\theta$. Since input x is 0, weight is irrelevant here.                           |
| -1  | 0.4 | decrease; | We want to be above base amount of $\theta$. Since input x is negative, decreasing weight will increase the product.  |

This results in the learning rule (also called delta rule): 
$\triangle \omega_i = \alpha x_i (y_\text{desired} - y)$
- This learning rule allows them to learn on any dataset; but note the solutions are not "unique"

Note: if implementing this in hardware:
- connect several motors with potentiometers; 
	- potentiometers: variable resistors whose resistance changes based on the position of a wiper. The position of the wiper can represent the weight (ωi\omega_iωi​) in the perceptron
	- motors: connected to the potentiometers to adjust their positions to adjust weight
