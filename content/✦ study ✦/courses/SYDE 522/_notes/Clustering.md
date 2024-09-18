This method is an example of unsupervised learning: Given a set of inputs, how do we figure out "good" groups in the data. 
![](https://media.geeksforgeeks.org/wp-content/uploads/merge3cluster.jpg)
The best way to find the patterns in data; to get our groupings is __distance__ between elements. 

There are three theories of how humans actually build categories: 
1. [[Prototype theory]]
   - Prototype-based clustering defines [[K-means clustering]]
2. [[Exemplar theory]]
   - Exemplar-based clustering defines [[Hierarchical clustering]]
3. [[Theory theory]]

However, what if we want our categories to have some structure? [[Kohonen Network]]

Note: Normalizing data is important before running clustering methods.
- By having both axes of data in the same scale, we can normalize a distance of "1" in each dimension