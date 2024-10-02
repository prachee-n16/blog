*Key terms*
- Parameters: values in the model that are set directly using the training data
	- weights, bias
- Hyperparameters: values in the model that are set separately
	- e.g. amount of regularization, # neurons, etc

**How to know if an AI model works?**
- Split the data sets into three distinct sets—**training**, **validation**, and **testing**.
	- Training set: Used to train the model.
		- model adjusts its internal parameters like "weights"
	- Validation set: Used for tuning hyperparameters (e.g., regularization strength, number of features, learning rate, etc.)
	- Testing set: Used for the final evaluation of the model's performance after training and validation are complete
- Typical split is 80% training, 20% testing
	- Use **cross-validation**, where the data is split into different test chunks (e.g., 5-fold or 10-fold cross-validation)
- Use validation data to set hyperparameters; training data to set parameters

To measure performance of a model,
- RMSE (Root mean squared error) metric where $$RMSE = \sqrt{\frac{1}{N}\Sigma(y_{target} - y)^2}$$
- Accuracy: percentage of "correct predictions" the model makes of all total predictions

So, to quantify: [[Model Evaluation Metrics]]