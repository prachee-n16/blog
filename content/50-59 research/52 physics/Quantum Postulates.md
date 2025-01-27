1. The state of a quantum mechanical system, including all the information you can know about it, is represented mathematically by a normalized ket $\ket{\psi}$ 
   - This state is a vector in Hilbert space, and it must be normalized to ensure the total probability is 1. 
2. A physical observable is represented mathematically by an operator A that acts on kets. 
   - Physical observable represents position, momentum or spin; also, correspond to mathematical operators.
   - When these operators act on state vector, they reveal measurable properties like eigenvalues?
3. The only possible result of a measurement of an observable is one of the eigenvalues $a_n$ of the corresponding operator $A$ 
   - When you measure an observable, the outcome is always one of the eigenvalues of the associated operator.
	   - The system “collapses” to an eigenstate corresponding to that eigenvalue after the measurement.
4. The probability of obtaining the eigenvalue $a_n$ in a measurement of the observable A on the system in the state $\ket{\psi}$ is $P_{a_n} = |\braket{a_n|\psi}|^2$   where $\ket{a_n}$ is the normalized eigenvector of A corresponding to the eigenvalue $a_n$.
5. After a measurement of that yields the result $a_n$, the quantum system is in a new state the is the normalized projection of the original system ket onto the ket (or kets) corresponding to the result of the measurement: $$\ket{\psi{'}} = \frac{P_n\ket{\psi}}{\sqrt{\braket{\psi|P_n|\psi}}}$$
6. The time evolution of a quantum system is determined by the Hamiltonian or total energy operator H(t) through the Schrodinger equation.