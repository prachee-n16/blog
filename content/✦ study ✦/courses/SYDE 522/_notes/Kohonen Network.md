also called Self-organizing map;

Roughly put,
- Generate a random set of prototypes for categories (just like centroids in [[K-means clustering]])
- Organize them into some structure where we define distance between categories
- Update the algorithm:
	- Randomly pick an input data point
	- Determine what category it is in
	- Move the prototype towards x and move nearby categories as well
- Start with a large nearby neighbourhood and reduce the nearby neighbourhood

Example: organizing RGB colors (3-dimensional) into a 2D map