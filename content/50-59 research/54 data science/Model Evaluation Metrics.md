> [!note] Key terms
> - True Negative (TN): correctly predicts a negative class (model says "no", result is "no")
> - True Positive (TP): correctly predicts a positive class (model says "yest", result is "yes")
> - False Negative (FN) - incorrectly predicts a negative class (model says "no", result is "yes")
> - False Positive (FP) - incorrectly predicts a positive class (model says "yes", result is "no")

**Performance metrics**
- **Sensitivity** or **recall**: We can measure how well a model identifies positive cases by:
$$TPR = \frac{TP}{TP+FN}$$
- **Specificity**: Similarly, we can measure how well a model identifies negative cases by:
$$TNR = \frac{TN}{TN+FP}$$
- Precision measures the accuracy of positive predictions:
$$Precision = \frac{TP}{TP+FP}$$
- Accuracy is the proportion of correct predictions out of the total predictions.
$$Accuracy = \frac{TN+TP}{TN+FP+FN+TP}$$
- Balanced accuracy is the average of sensitivity and specificity i.e. True positive rate and true negative rate
$$\text{Balanced Accuracy} = \frac{TPR+TNR}{2}$$
- F1 Score is the "harmonic" mean of precision and recall. It focus on when both precision (how correct the yes predictions are) and recall (how often the system identifies yes)
$$F1 = \frac{2\times TP}{2\times TP + FP+FN}$$

**ROC Curve** (Receiver Operating Characteristic)
- plots the true positive rate (sensitivity) against the false positive rate at various threshold settings
	- diagonal line represents a model with no skill, predicting randomly.
	- the goal is to choose a model that achieves 100% true positive rate and 0% false positive rate.

![](https://miro.medium.com/v2/resize:fit:1200/1*Bgc9QOjhnL70g2SQxyj6hQ.png)
