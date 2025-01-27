Notes: ![[Quantum Annealing.pdf]]
**Overview**
- **Quantum Annealer**: special purpose quantum computer; 
	- It is different from General Purpose Quantum Computers which can be freely programmed from computers
	- Instead, it is designed & built to host a single quantum algorithm, **Quantum Annealing**
- Quantum annealing (QA) is a heuristic optimization technique used to find the global minimum of a problem's energy landscape. It uses quantum mechanics, particularly quantum tunneling and superposition, to explore solutions.
	- Simply put,  quantum algorithm capable of solving optimization problems
		- It is particularly useful for solving combinatorial optimization problems and challenges in discrete mathematics, such as factoring large numbers, solving SAT problems, or optimizing logistics.
- A little bit about the history:
	- In 1998, this paper introduced the concept: https://arxiv.org/abs/cond-mat/9804280
		- Written by Professor Hidetoshi Nishimori who works as a full professor at the University of Tokyo
	- However, the first Quantum Annealer model from **D-Wave** i.e. physical implementation came out in 2012

**Classical Algorithm**
- Suppose we have an optimization problem, for example a **minimization problem** where there is a function to be minimized; 
	- *Objective function* - the function to be minimized; it is known and computable using a finite set of variables
- Best way to solve a minimization problem is the **brute-force approach**
	- calculate all the values for all possible inputs and consider the smallest
	- this isn't a great approach if you have a lot of inputs (for N inputs, that is $2^N$ combinations)
- **Simulated Annealing**: probabilistic strategy used to solve optimization problems
	- Think of this analogy: a ball rolls along the graph of a function, falling into the holes defined by the minima
		- Every time a ball lands in a hole it receives a certain amount of energy, enough to make it jump over another piece of graph, looking for deeper minima points.
![[Screenshot 2024-11-24 at 11.48.03 AM.png|500]]

**Quantum Algorithm**
![[Screenshot 2024-11-24 at 11.49.44 AM.png|500]]
**Methodology**
- **Representation of Problems**:
	- We previously introduced an **objective function** - this is really just a mathematical expression of the energy of a system
		- We want to find the minimum of this function; i.e. lowest energy of a system;
		- If the solver is a QPU, this is a function of the binary variables that represent its qubits; If the solver is a classical quantum hybrid solver, energy might be an abstract function
	- So, first, **problems are mapped to a Hamiltonian** (a mathematical object representing the total energy of a quantum system). 
	- Next, the goal is to convert all our problems into **minimization problems**.
		- Example: x + 1 = 2 can be rewritten as: $min[2 - (x + 1)]^2$ 
	- The goal is to encode the problem into an **Ising model** or **quadratic unconstrained binary optimization (QUBO)** form. See more below.
		- Any QUBO problem can be easily mapped into an ISING problem through simple equivalence
		- Note: *PyQUBO is a python library, with a C ++ backend, written by DWAVE to use its quantum annealer.* 
- **Hamiltonian Dynamics**:
	- The system begins in a simple initial Hamiltonian $H_{\text{initial}}$, where the ground state is easily achievable.
	- Over time, it evolves into the problem Hamiltonian $H_{\text{problem}}$ where the ground state represents the optimal solution.
	- It depends on the **adiabatic theorem** where if a system starts in the ground state of an initial Hamiltonian and the Hamiltonian evolves slowly enough, the system will remain in the ground state of the evolving Hamiltonian.

	- The initial Hamiltonian is chosen to have a simple ground state that is easy to prepare
		- Usually, it represents a superposition of all possible states: $H_{\text{initial}} = -\Sigma_i \Delta_i \sigma_i^x$    
		- Physically, this means in this state, all qubits (spins) are in a uniform superposition of $\ket{0}$ and $\ket{1}$
		- This allows the system to "explore" all possible solutions simultaneously due to quantum superposition.

	- We want to evolve into the problem Hamiltonian which is our optimization problem (in Ising model or QUBO format). Its ground state corresponds to the solution to the problem.
		- Physically, this Hamiltonian describes the energy of the system; and the global minimum represents the optimal solution.

	- The system's Hamiltonian evolves smoothly over time as:

- **Quantum Tunneling**:
	- Unlike classical algorithms, QA exploits **quantum tunneling** to traverse energy barriers in the landscape, finding solutions faster when stuck in local minima.

**Ising Model** is a well-known model in statistical mechanics. 
- an Ising Hamiltonian has as variables +1 and -1 which relate to spin variables (+1 is spin up, -1 is spin down)
- The relationships between the spins, represented by the coupling values of the Hamiltonian, represent the correlations or anti-correlations
	- essentially, how individual qubits (or spins) interact with each other
- Mathematically, the energy of the system is $H=∑_i​h_i​s_i​+∑_{i<j}​J_{ij}​s_i​s_j​$  
	- coefficients h represent the bias values associated with the qubits  
	- coefficients J represent the strength of the coupling bonds

**QUBO** problem is defined by a matrix Q (upper triangular) and a vector of binary variables x.
- The mathematical form of a QUBO (Quadratic Unconstrained Binary Optimization) problem is given as: $$f(x) = \sum_{i} a_i x_i + \sum_{i<j} b_{ij} x_i x_j$$
	- $x \in {0, 1}$ are binary variables 
	- $a_{ij}$ are linear coefficients, $b_{ij}$ are quadrating coefficients

To convert from the **Ising model** to the **QUBO (Quadratic Unconstrained Binary Optimization)**: https://dominicplein.medium.com/qubo-and-ising-equivalence-65275a4f4f39


