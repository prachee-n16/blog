The Pauli matrices are a set of 2x2 complex matrices that are used to represent the spin operators for spin-1/2 particles. These matrices are used to describe spin along different directions—typically x, y, and z axes.

Pauli matrices are: 
![300](https://miro.medium.com/v2/resize:fit:1346/1*ckd_S58HytLcDRKeKqZlvg.png)

In fact, to calculate spin [[Operators|operator]] in a general direction $\hat{S_n}$:
- General direction $\hat{n}$ is expressed as a combination of vectors in the x, y, and z directions: $$\hat{n}=\hat{i}\text{ sin }\theta cos\phi + \hat{j}\text{ sin }\theta \text{ sin }\phi + \hat{k}\text{ cos }\theta$$
- The spin operator in the direction $\hat{n}$: $$\hat{S}_n = \hat{S}_x \text{ sin }\theta \text{ cos }\phi + \hat{S_y}\text{ sin }\theta\text{ sin }\phi+\hat{S_z}\text{ cos }\theta$$
- When expressed in matrix form, $$\hat{S}_n = \frac{\hbar}{2} \begin{pmatrix} \cos\theta & \sin\theta e^{-i\phi} \\ \sin\theta e^{i\phi} & -\cos\theta \end{pmatrix}$$
For eigenvalues - $\lambda = \pm \frac{\hbar}{2}$; and eigenvectors:
$$|+\rangle_n = \cos\frac{\theta}{2} |+\rangle + \sin\frac{\theta}{2} e^{i\phi} |-\rangle = \begin{pmatrix} \cos\frac{\theta}{2} \\ \sin\frac{\theta}{2} e^{i\phi} \end{pmatrix}$$
$$|-\rangle_n = \sin\frac{\theta}{2} |+\rangle - \cos\frac{\theta}{2} e^{i\phi} |-\rangle = \begin{pmatrix} \sin\frac{\theta}{2} \\ -\cos\frac{\theta}{2} e^{i\phi} \end{pmatrix}$$
