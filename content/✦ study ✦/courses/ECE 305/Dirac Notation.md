[[Quantum Postulates|Postulate]] 1 states that: The state of a quantum mechanical system, including all the information you  
can know about it, is represented mathematically by a normalized ket $\ket{\psi}$ 

$\ket{\psi}$ - quantum state vector, part of a vector space called **Hilbert space**
- In 2-D space of a spin $\frac{1}{2}$ system, the two kets $\ket{\pm}$ form a [[Basis|basis]]; completeness of this basis implies that a general quantum state vector $\ket{\psi}$ is a linear combination of two basis kets:
  $$\ket{\psi} = a\ket{+} + b\ket{-}$$

> [!note] Note
> General quantum state vector is not a wave function; $\psi(x)$ is a quantum mechanical wave function. Kets don't have any "spatial dependence" as wave functions do

The analog to ket notation is **bra**:
  $$\bra{\psi} = a^*\bra{+} + b^*\bra{-}$$
The scalar product in quantum mechanics, or more commonly referred to as **inner product** and **projection** is defined as: $\braket{\text{bra|ket}}$     
- When finding inner products of basis vectors $\braket{+|+}$, since these are unit vectors, $\braket{+|+}$ = 1
- Similarly, for orthogonality, $\braket{+|-}$ = 0

In summary, the properties are: 
![[Properties of Quantum Basis.png|400]]

Consider a general state vector, using the properties above, here are derivation of other properties:
**Property 1**: 
![[Property of Quantum State Vector 1.png|300]]
![[Property of Quantum State Vector 3.png|300]]
**Property 2:**
![[Property of Quantum State Vector 2.png|300]]

**Key Problem**: Normalize a quantum state vector.
![[Normalization Quantum State Vector Example.png]]

