Widely used in the [[SVM]] model to bridge linearity and non-linearity. 

The general idea is that with enough features, everything becomes linearly separable.
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRSs1L83ejgcQ6f0L0qNSt3xFInb9KuulyIUg&s)
For example, the circular trend is not linearly classifiable but adding a dimension allows us to transform this to a linear problem. 
- it lets find the optimal separating hyperplane in this higher dimension, which is what we need for our linear SVM's to work
- many transformations exist which allow the data to be linearly separated in higher dimensions, 
	- not all of these functions are actually kernels!!

**Kernel** - a function that takes as it's inputs vectors in the original space and then, returns the dot product of the vectors in the feature space
- we take inputs in lower dimensional space and return the dot product of the new vectors in higher dimensions
