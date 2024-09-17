Core of most AI is "function approximation".
- Given an input, I want to accurately predict the output; Essentially, find the best mapping 

These mappings can involve problems like:
- Classification: here's a set of inputs; each of which needs to be labelled with a category.
	- Example: Identify dogs vs cats from a set of unlabelled data
	- In supervised learning, it can be expensive to get those labels and there's the problem of accuracy in labelling
- Function Approximation or Regression: here's a set of inputs, each of which needs a desired numerical output
	- Example: Here are some characteristics of a gem; determine it's worth (price)
	- Still supervised learning but expensive to get those values
- Clustering: Here's a set of inputs, figure out good groups
	- It's unsupervised learning but how do we know if it's useful groupings
- Dimensionality Reduction: Compress but keep information
	- Unsupervised learning but how do we know it's useful organizing
- Reinforcement Learning: Given an input of the current situation, output the action to take
	- It generates feedback i.e. a numerical value of how good or bad your actions have been
		- Usually 0 most of the time, 1 if you succeed (reinforces this action)

In addition to supervised and unsupervised learning,
- Semi-supervised
	- Getting labelled data is hard so, let's only label some of it
	- This makes it a mixture of supervised and unsupervised
- Self-supervised
	- The task is such that desired output data is in training data itself
		- Example: given the previous 10 words, predict the next word
	- No extra effort to label the data; still supervised