### Motivation
How can I optimize "things"? Well, what are these "things"? It can be any of this:
- A mathematical function $$\frac{-x^2}{10}+3x$$
- A puzzle like N-queens (placing 8 queens on a chessboard so none can capture each other)
- Neural network connection weights - Find the weights that minimize the difference between output and target
- Neural network arch. - Find the structure that after training with backprop. will minimize the difference between output and target

Well, to begin optimizing:
- given a candidate solution, we want to quantify how good that solution is? Terminology: **Fitness function**
	- $\frac{-x^2}{10}+3x$ is the fitness function; yay!
	- It's a bit more difficult for placing 8 queens on a chessboard so none can capture each other
		- How can we score this? If we can capture it, let's say it's 1; else, it's 0
	- For this problem, find the weights that minimize the difference between output and target
		- Fitness function becomes - Make a prediction using the network and measure the difference; i.e. MSE essentially
	- For this problem, find the structure that after training with backprop. will minimize the difference between output and target
		- Fitness function can be same as previous; use MSE with early stopping to fix our issue

How do I **optimize** things?
- Methods:
	- Take the derivative, set it to zero, solve
		- Only works if the function is differentiable and solvable
	- Take the derivative, make learning rule out of that and iteratively apply learning rule
		- This is the basis of backpropagation; It still needs to be differentiable and solvable
	- Brute-force approach; try every option which can be very expensive
	- Random search;
	- **Genetic algorithm**

The caveat is genetic algorithm is going to be a random search with some heuristics;

### Genetic Algorithm
- How does **biological evolution** find good solutions? Lots of trial and error; 
	- If we are given a population of individuals, each one is a different candidate solution
	- The higher the **fitness**, the higher the chance of producing offspring
		- Each offspring is a new individual; that individual is produced by combining the parent's solution plus some random mutation
	- Repeat this process and individual solutions improve.
- It does introduce some questions:
	- What is the population size? What do we mean by random mutation? How do we combine from each parent? 
