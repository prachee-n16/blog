Regression is the problem of finding **w** (weights) that fits the relationship between input **x** and output **y**.

*Linear Regression*
Use the method of least squares to solve for weight vector $W$. 

Consider:
- matrix of input data $X$ of dimensions $m \times n$ where m is number of data points and n is number of features
- $W$ is the weight vector of dimensions $n \times 1$ 
- $Y$ is the output or target values of dimensions $m \times 1$

In the linear regression model, we're trying to find $W$ such that: $XW = Y$

$X$ might not be a square matrix i.e. not invertible. However, $X^TX$ is a square matrix with dimensions $n \times n$ 
$$X^TXW = X^TY$$
Taking the inverse of $X^TX$,
$$(X^TX)^{-1}(X^TX)W = (X^TX)^{-1}X^TY$$
Since $(X^TX)^{-1}(X^TX)$ simplifies to the identity matrix,
$$W = (X^TX)^{-1}X^TY$$
This resultant matrix is also the **pseudoinverse of $X$** 

The goal is to find the weight vector that minimizes the sum of squared differences between the predicted and actual values. 

The cost function, or MSE (mean squared error) is

$E(w) = \frac{1}{2}\Sigma_n(y_n - w^Tx_n)^2$ 

If we solve for $w$, we get the same form as above.



Related: [[multipleLinearRegression | Multiple Linear Regression]]