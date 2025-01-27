Consider the **the bias-variance tradeoff in KNN**

- tradeoff between underfitting and overfitting
- In the context of **K-Nearest Neighbors (KNN)**, the choice of the hyperparameter kk plays a crucial role
  - **Low k:** High variance, low bias
    - Decision boundary is very flexible.
    - Captures more noise in the data.
    - May perform well on training data but poorly on unseen data.
  - **High k:** Low variance, high bias
    - Decision boundary is smoother.
    - Less sensitive to noise but may miss key patterns in the data.
    - May generalize better but might not perform well if the decision boundary is complex.

**Idea**: train classifiers on separate training data and use the average of all their data;

- This is kind of the idea behind **ensemble learning** but we need a lot of training data;

**Ensemble learning** is a machine learning technique where multiple models (often referred to as "weak learners") are combined to create a single, more robust model (a "strong learner")

- **Reduce variance**: Combines models to reduce overfitting and increase generalization.
- **Reduce bias**: Combines weak models to better approximate the true data distribution.
- **Improve robustness**: Averages out errors from individual models, making predictions more stable.
  Multiple models are trained independently on different subsets of the training data created via **bootstrap sampling** (sampling with replacement).
- some data may be selected again, while some data points are left entirely;
  **Confidence interval** --> helpful in bootstrapping!

Key words: Bagging (bootstrap aggregation);

Neuromorphic Hardware

- **Carver Mead and Lynn Conway**: GOAT on reliably designing microelectronic circuits..
