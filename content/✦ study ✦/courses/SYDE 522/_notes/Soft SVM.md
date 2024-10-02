Background: [[SVM]]
**Soft SVM** is a modified version of the original SVM that allows for some classification errors while still maximizing the margin.

In **Hard SVM**, the constraint is strict: $y_i(wx_i + b) > 1$ where every point has to be on the correct side of the margin
- Instead, we introduce a slack variable $\xi_i$ that allows some points to fall within the margin
$$y_i(wx_i + b) \geq 1 - \xi_i$$
