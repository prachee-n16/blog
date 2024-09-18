Roughly put,
- Each data points starts as it's own category
- Merge the closest 2 together into a single category
	- Distance between two categories is the shortest distance between two points in that category 
- Continue repeating this action of merging

![500](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ0C8UITUD6RLasOoJlYVe58ZMSd7lQBvqNYg&s)
Since we want to merge the **closest two points**, we need to build a table that shows the distance between each pair of points. 

We can also visualize this clustering using a **dendrogram**: 
![](https://miro.medium.com/v2/resize:fit:740/1*VvOVxdBb74IOxxF2RmthCQ.png)

