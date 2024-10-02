Regularization refers to any method that makes the accuracy on the training data worse but improves performance on unknown test data.
- This reduces [[Overfitting|overfitting]] by preventing it from fitting noise

In this error function (as seen for [[Regression|regression]]),
$E(w) = \frac{1}{2}\Sigma_n(y_n - w^Tx_n)^2$ 

With regularization, 
$E(w) = \frac{1}{2}\Sigma_n(y_n - w^Tx_n)^2 + \lambda\frac{1}{2}||w||^2$ 
- The regularization term where $||w||^2$ penalizes large weights and $\lambda$ controls trade-off between fitting data and penalizing large weights

This is equivalent to adding gaussian noise where we introduce small random disturbances.