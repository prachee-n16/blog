Related: [[Soft SVM]]

Supervised learning models used for classification by finding the hyperplane that separates data into different classes
- Hyperplane: In a N-dimensional space, hyperplane has N-1 dimensions. So, in the 2-D plane, this is simply a line.
Data points on one side of the hyperplane are in one class, while other side belong to another class.

For SVM with non-linear boundary: [[Kernel Trick]]

![](https://camo.githubusercontent.com/b8479e60b9eabf83fb6754e06a929a94b9f8e6a2ea885668c61a0e558e361837/68747470733a2f2f666972656261736573746f726167652e676f6f676c65617069732e636f6d2f76302f622f6465762d737461636b2d6170702e61707073706f742e636f6d2f6f2f73766d25324673766d2d6d696e2d6d696e2e706e673f616c743d6d6564696126746f6b656e3d64346636323530662d376531622d346538382d613831392d666563323430363136306263)

The goal of the SVM is to maximize the margin; 
- Margin i.e. distance between the decision boundary (hyperplane)  
	- measure of how well-separated the classes are in feature space
- the data points closes to decision boundary are **support vectors**; which are used to calculate margin

To maximize the margin of length $\frac{b}{||w||}$, we need to minimize $w$.
- Constrained Optimization Problem - Minimize $E(w) = \frac{1}{2}||w||^2$ subject to $y_i(wx_i + b) > 1$ 

The optimal solution depends on support vectors (data points that lie on the margin). Weight vector is a weight sum of the support vectors:
$$w = \sum_i\alpha_iy_ix_i$$

The weight vector $w$ is expressed as a weighted sum of the training data points, but only the support vectors influence this sum. 
- This is an example of the **Representer Theorem**, which applies to kernel methods like SVMs.

