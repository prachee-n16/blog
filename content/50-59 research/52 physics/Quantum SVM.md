Classically, I know how SVM works (part of AI material). 
- Support Vector Machine (SVM) is a supervised machine learning model used for **classification** and **regression** tasks
- key idea is to find a **hyperplane** that best separates data points belonging to different classes with the maximum margin
To handle non-linearly separable data, the **kernel trick** is used to transform the data into a higher-dimensional space where a linear hyperplane can separate the classes.

**In detail, classical SVM is:**
The optimization problem in a classical SVM can be formulated as:

$$
\min_{w, b} \frac{1}{2} \|w\|^2
$$

Subject to:

$$
y_i (w^T x_i + b) \geq 1, \quad \forall i
$$

Here:
- $w$ is the weight vector.
- $b$ is the bias term.
- $y_i$ is the label (\($+1$\) or \($-1$\)) for each data point $x_i$.
- The goal is to find the optimal hyperplane \( $w^T x + b = 0$ \) that separates the data points with the maximum margin.

In the **dual formulation**, we introduce Lagrange multipliers  $\alpha_i$ and solve:

$$
\max_{\alpha} \sum_{i=1}^{n} \alpha_i - \frac{1}{2} \sum_{i=1}^{n} \sum_{j=1}^{n} \alpha_i \alpha_j y_i y_j K(x_i, x_j)
$$

Subject to:

$$
\sum_{i=1}^{n} \alpha_i y_i = 0, \quad 0 \leq \alpha_i \leq C, \quad \forall i
$$

Here, $K(x_i, x_j)$ is the kernel function that computes the inner product in a higher-dimensional feature space.

## Quantum SVM
- we leverage quantum mechanics to transform data into a much **higher-dimensional space** using quantum states. 
- The idea is to use a **quantum computer** to calculate a **quantum kernel** efficiently.

#### Quantum Feature Map

In the classical SVM, we use a kernel function \( $K(x, x')$ \) to implicitly transform data into a high-dimensional space. In Quantum SVM, we use a **quantum feature map** to encode classical data $x$ into a quantum state $\phi(x) \rangle$

This is done using a **quantum circuit** that takes the input data \( x \) and converts it into a quantum state:

$$
\phi(x) \rightarrow | \phi(x) \rangle
$$

The data is thus mapped into a **Hilbert space** (a very high-dimensional space) that a quantum computer can efficiently process.

Once the data is encoded into quantum states, the next step is to compute the **quantum kernel**. This kernel is defined as the **inner product** of two quantum states:

$$
K(x, x') = |\langle \phi(x) | \phi(x') \rangle|^2
$$

Here:

- $| \phi(x) \rangle$ is the quantum state corresponding to data point \( x \).
- $\langle \phi(x) | \phi(x') \rangle$ is the inner product (overlap) between two quantum states.
- The squared modulus $|\langle \phi(x) | \phi(x') \rangle|^2$ gives a similarity measure between the two data points in the quantum space.

**METHODOLOGY**

1. **Data Encoding**: For each data point $x$, a quantum circuit is constructed to encode $x$ into a quantum state $| \phi(x) \rangle$.
  
2. **Kernel Estimation**: To compute the kernel value $K(x, x')$, we use a quantum computer to measure the overlap between two quantum states:

   $$
   K(x, x') = |\langle \psi(x) | \psi(x') \rangle|^2
   $$

   This involves preparing the quantum states $| \psi(x) \rangle$ and $| \psi(x') \rangle$, and then measuring their overlap using quantum measurements.

3. **Training the SVM**: The kernel values computed by the quantum computer are then used in the classical SVM optimization process:

   $$
   \max_{\alpha} \sum_{i=1}^{n} \alpha_i - \frac{1}{2} \sum_{i=1}^{n} \sum_{j=1}^{n} \alpha_i \alpha_j y_i y_j K(x_i, x_j)
   $$

   Subject to:

   $$
   \sum_{i=1}^{n} \alpha_i y_i = 0, \quad 0 \leq \alpha_i \leq C, \quad \forall i
   $$

4. **Prediction**: Once the model is trained, we can classify a new data point $z$ by computing:

   $$
   f(z) = \sum_{i=1}^{n} \alpha_i y_i K(x_i, z) + b
   $$

   Here, $K(x_i, z)$ is the quantum kernel computed using the overlap between the quantum states for $x_i$ and $z$.