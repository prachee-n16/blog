Principal Component Analysis is a **dimensionality reduction** method
- Essentially, we want to reduce the number of variables of a data set! Why? It makes analyzing data easier and faster for ML algorithms without looking at extraneous variables.
	- An extraneous variable is **any variable that you're not investigating that can potentially affect the dependent variable of your research study**.
	- More solid reason: We can't visualize 6 axes at the same time (max. 3) but if we can combine some axes together in a "smart" way, that would be amazing!!
- So, to sum up, the idea of PCA is simple: **reduce the number of variables of a data set, while preserving as much information as possible.**

- Principal components are **new variables** that are created by combining the original variables in a specific way.
	- Think of them as a new set of axes that better represent the underlying structure of the data.

### Classical PCA
- Standardization
	- standardize the range of the continuous initial variables so that each one of them contributes equally to the analysis
		- if there are large differences between the ranges of initial variables, those variables with larger ranges will dominate over those with small ranges
		- for example, a variable that ranges between 0 and 100 will dominate over a variable that ranges between 0 and 1 (BIAS~)
	- mathematically, $z = \frac{\text{value-mean}}{\text{standard deviation}}$ 
- Covariance Matrix Computation
	- understand how the variables of the input data set are varying from the mean with respect to each other
	- sometimes, variables are highly correlated in such a way that they contain redundant information
	- this matrix tells us that:
		- if it's positive: two variables increase or decrease together (correlated)
		- if it's negative: one increases when the other decreases (inversely correlated)
- Compute the eigenvectors and eigenvalues of the covariance matrix to identify the principal components
	- **eigenvectors and eigenvalues who are behind all the magic of principal components**
	- eigenvectors of the Covariance matrix are actually _the_ _directions of the axes where there is the most variance_
		- Principal Components! 
	- By ranking your eigenvectors in order of their eigenvalues, highest to lowest, you get the principal components in order of significance.
- then, we discard those with low significance and only use those with high significance!

**Why classical computers struggle?**
==**PROBLEM 1:** calculation of eigenvectors and eigenvalues==
- The higher the dimensionality of the input, the larger the set of corresponding eigenvectors and eigenvalues.
- Quantum computers can solve this problem very efficiently!

### qPCA
1. Quantum State Preparation: Prepare a quantum state that encodes the data to be analyzed. This can be done using techniques like quantum random access memory (QRAM) or quantum data loading.
2. Quantum Phase Estimation: Use quantum phase estimation to estimate the eigenvalues of the covariance matrix.
3. Quantum Fourier Transform: Apply a quantum Fourier transform to extract the principal components.
4. Measurement: Measure the quantum state to obtain the classical results.

Note: each topic here is a beast..