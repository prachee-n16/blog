Roughly speaking, 
- We partition our dataset into `k` prototypes (randomly selected).
- We classify items into one of the `k` groups defined previously.
- Then, update the prototypes by taking an average. We run multiple iterations until we stabilize with the groups.

The loss function:
$$E = \sqrt{\frac{1}{N}\sum_k\sum_i||x_i-c_k||^2}$$
- We measure the squared euclidean distance between the points to the centroid (i.e. center of the cluster) 
	- By summing over every cluster, we measure the total variance within the clusters
- Divide by N (i.e. total number of data points) for *normalization* to get the average variance
- Why square root? Gives us the average distance in the original Euclidean space
In short, we are computing RMSE of the clustering process. 

It can result in multiple solutions; sometimes categorizing incorrectly. To choose the right `k` for our algorithm, we can use the **elbow method**.
- To determine the k-value we continuously iterate for k=1 to k=n (n being the hyperparameter we choose as per requirement)
- For every value of k, we calculate the within-cluster sum of squares (WCSS) value
	- i.e. sum of square distance between centroids and points
- For determining the best number of clusters(k) we plot a graph of k versus their WCSS value
- When k=1 the WCSS has the highest value but with increasing k value WCSS value starts to decrease
- choose that value of k from where the graph starts to look like a straight line

