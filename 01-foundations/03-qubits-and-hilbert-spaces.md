# Qubits and Hilbert Spaces

## 1. Why Hilbert space is the right language

Quantum mechanics needs a space in which states can be added coherently, compared through inner products, transformed linearly, and measured. For finite-dimensional quantum information, that space is a finite-dimensional complex Hilbert space.

For a single qubit,

```math
\mathcal H\cong\mathbb C^2.
```

For $n$ qubits,

```math
\mathcal H_n=(\mathbb C^2)^{\otimes n}.
```

The Hilbert-space viewpoint is more fundamental than any particular hardware implementation. A superconducting qubit, trapped-ion qubit, spin qubit, or photonic encoding can all implement the same abstract two-dimensional state space.

### Learning objectives

After this chapter, you should be able to:

- use bra-ket notation fluently,
- distinguish vectors, operators, and observables,
- work with orthonormal bases and changes of basis,
- derive the general pure-qubit parameterization,
- explain why global phase is redundant,
- characterize unitary, Hermitian, positive, and projective operators,
- use Pauli matrices as an operator basis,
- connect Hamiltonians to unitary time evolution,
- and compute basic expectation values and eigenstates.

---

## 2. Complex vector spaces and inner products

A finite-dimensional Hilbert space is a complex vector space equipped with an inner product.

For vectors $|\phi\rangle$ and $|\psi\rangle$, the inner product is written

```math
\langle\phi|\psi\rangle.
```

It is conjugate-linear in the first argument and linear in the second. In coordinates,

```math
|\psi\rangle=
\begin{pmatrix}
\psi_1\\
\vdots\\
\psi_d
\end{pmatrix},
\qquad
\langle\phi|
=
\begin{pmatrix}
\phi_1^*&\cdots&\phi_d^*
\end{pmatrix},
```

so

```math
\langle\phi|\psi\rangle
=
\sum_{j=1}^d \phi_j^*\psi_j.
```

The induced norm is

```math
\|\psi\|
=
\sqrt{\langle\psi|\psi\rangle}.
```

A pure quantum state is represented by a normalized vector:

```math
\langle\psi|\psi\rangle=1.
```

---

## 3. Bra-ket notation

A **ket** $|\psi\rangle$ is a vector. Its dual vector is the **bra** $\langle\psi|$.

For

```math
|\psi\rangle=
\begin{pmatrix}
\alpha\\
\beta
\end{pmatrix},
```

we have

```math
\langle\psi|
=
\begin{pmatrix}
\alpha^*&\beta^*
\end{pmatrix}.
```

The outer product

```math
|\psi\rangle\langle\phi|
```

is not a scalar. It is an operator. For example,

```math
|0\rangle\langle1|
=
\begin{pmatrix}
0&1\\
0&0
\end{pmatrix}.
```

This distinction is used constantly in density matrices, projectors, controlled gates, and quantum channels.

---

## 4. Bases and completeness

An orthonormal basis $\{|e_j\rangle\}_{j=1}^d$ satisfies

```math
\langle e_j|e_k\rangle=\delta_{jk}.
```

Every vector can be expanded as

```math
|\psi\rangle
=
\sum_j c_j|e_j\rangle,
```

where

```math
c_j=\langle e_j|\psi\rangle.
```

An orthonormal basis satisfies the completeness relation

```math
\sum_j |e_j\rangle\langle e_j|=I.
```

This identity is one of the most useful algebraic tools in quantum information. It allows us to insert a basis resolution without changing an expression.

---

## 5. The qubit

The state space of one qubit is

```math
\mathcal H_2\cong\mathbb C^2.
```

The computational basis is

```math
|0\rangle=
\begin{pmatrix}
1\\
0
\end{pmatrix},
\qquad
|1\rangle=
\begin{pmatrix}
0\\
1
\end{pmatrix}.
```

A general pure qubit is

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle,
```

with

```math
|\alpha|^2+|\beta|^2=1.
```

The pair $(\alpha,\beta)$ contains four real numbers. However, not all four correspond to physical degrees of freedom.

---

## 6. Deriving the two-parameter pure-qubit form

Write the amplitudes in polar form:

```math
\alpha=r_0e^{i\gamma_0},
\qquad
\beta=r_1e^{i\gamma_1}.
```

Normalization gives

```math
r_0^2+r_1^2=1.
```

We can therefore parameterize

```math
r_0=\cos\frac\theta2,
\qquad
r_1=\sin\frac\theta2,
```

with $0\le\theta\le\pi$.

The state is

```math
|\psi\rangle
=
e^{i\gamma_0}
\left(
\cos\frac\theta2|0\rangle
+
e^{i(\gamma_1-\gamma_0)}
\sin\frac\theta2|1\rangle
\right).
```

Define

```math
\phi=\gamma_1-\gamma_0.
```

The common factor $e^{i\gamma_0}$ is a global phase and does not affect physical predictions. Therefore every pure qubit can be represented as

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle,
```

with

```math
0\le\theta\le\pi,
\qquad
0\le\phi<2\pi.
```

This derivation explains why a pure qubit has exactly two independent real physical parameters. Those two parameters become the polar and azimuthal angles of the Bloch sphere.

---

## 7. States are rays, not vectors with absolute phase

If

```math
|\psi'\rangle=e^{i\gamma}|\psi\rangle,
```

then for any observable $A$,

```math
\langle\psi'|A|\psi'\rangle
=
\langle\psi|A|\psi\rangle.
```

Thus

```math
|\psi\rangle
\sim
e^{i\gamma}|\psi\rangle.
```

The physical pure state corresponds to a one-dimensional ray in Hilbert space.

This point becomes important when counting parameters, defining state distances, and understanding projective Hilbert space.

---

## 8. Linear operators

A linear operator is a map

```math
A:\mathcal H\rightarrow\mathcal H
```

satisfying

```math
A(a|\psi\rangle+b|\phi\rangle)
=
aA|\psi\rangle+bA|\phi\rangle.
```

The adjoint $A^\dagger$ is defined through

```math
\langle\phi|A|\psi\rangle
=
\langle A^\dagger\phi|\psi\rangle.
```

In matrix representation, $A^\dagger$ is the conjugate transpose.

### Important operator classes

A **unitary operator** satisfies

```math
U^\dagger U=UU^\dagger=I.
```

A **Hermitian operator** satisfies

```math
A=A^\dagger.
```

A **positive semidefinite operator** satisfies

```math
\langle\psi|A|\psi\rangle\ge0
```

for all $|\psi\rangle$.

A **projector** satisfies

```math
P=P^\dagger,
\qquad
P^2=P.
```

Each class has a different role:

- unitary operators describe reversible closed-system dynamics,
- Hermitian operators represent observables,
- positive operators appear in states and POVMs,
- projectors represent subspaces and projective measurement outcomes.

---

## 9. Why unitaries preserve quantum states

Suppose

```math
|\psi'\rangle=U|\psi\rangle.
```

Then

```math
\langle\psi'|\psi'\rangle
=
\langle\psi|U^\dagger U|\psi\rangle.
```

If $U$ is unitary,

```math
\langle\psi'|\psi'\rangle
=
\langle\psi|\psi\rangle.
```

Thus normalization is preserved.

Unitaries also preserve inner products:

```math
\langle U\phi|U\psi\rangle
=
\langle\phi|\psi\rangle.
```

Therefore they preserve angles, orthogonality, and distinguishability between pure states.

---

## 10. Hermitian operators and spectral decomposition

Every finite-dimensional Hermitian operator can be written as

```math
A=\sum_j a_j P_j,
```

where the eigenvalues $a_j$ are real and $P_j$ projects onto the corresponding eigenspace.

For a nondegenerate spectrum,

```math
A=\sum_j a_j|a_j\rangle\langle a_j|.
```

The real spectrum is why Hermitian operators are appropriate for observables.

If a pure state is measured in the eigenbasis of $A$, the probability of obtaining eigenvalue $a_j$ is

```math
P(a_j)=|\langle a_j|\psi\rangle|^2.
```

The expectation value is

```math
\langle A\rangle
=
\langle\psi|A|\psi\rangle
=
\sum_j a_jP(a_j).
```

---

## 11. The Pauli basis

The Pauli matrices are

```math
X=
\begin{pmatrix}
0&1\\
1&0
\end{pmatrix},
\qquad
Y=
\begin{pmatrix}
0&-i\\
i&0
\end{pmatrix},
\qquad
Z=
\begin{pmatrix}
1&0\\
0&-1
\end{pmatrix}.
```

Together with

```math
I=
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix},
```

they form a basis for all $2\times2$ complex matrices.

Any one-qubit operator can therefore be expanded as

```math
A=a_0I+a_xX+a_yY+a_zZ.
```

If $A$ is Hermitian, the coefficients can be chosen real.

The coefficients follow from Hilbert-Schmidt orthogonality:

```math
\mathrm{Tr}(\sigma_j\sigma_k)=2\delta_{jk},
```

where

```math
\sigma_0=I,
\quad
\sigma_1=X,
\quad
\sigma_2=Y,
\quad
\sigma_3=Z.
```

Hence

```math
a_j=\frac12\mathrm{Tr}(\sigma_jA).
```

This identity later becomes the basis of Pauli decomposition for Hamiltonians and observable estimation.

---

## 12. Pauli algebra

The Pauli matrices satisfy

```math
X^2=Y^2=Z^2=I.
```

Their products obey

```math
XY=iZ,
\qquad
YZ=iX,
\qquad
ZX=iY.
```

Reversing the order changes the sign:

```math
YX=-iZ.
```

Therefore

```math
[X,Y]=2iZ,
```

and cyclic permutations give

```math
[Y,Z]=2iX,
\qquad
[Z,X]=2iY.
```

They also anticommute pairwise:

```math
\{X,Y\}=\{Y,Z\}=\{Z,X\}=0.
```

This algebra underlies single-qubit rotations, spin observables, and many Hamiltonian constructions.

---

## 13. Hamiltonians and unitary time evolution

For a time-independent Hamiltonian $H$, Schrödinger evolution is

```math
|\psi(t)\rangle
=
e^{-iHt/\hbar}|\psi(0)\rangle.
```

The time-evolution operator is

```math
U(t)=e^{-iHt/\hbar}.
```

Because $H$ is Hermitian,

```math
U^\dagger(t)
=e^{iHt/\hbar},
```

so

```math
U^\dagger(t)U(t)=I.
```

Thus Hermitian generators produce unitary evolution.

In quantum-computing notation one often sets $\hbar=1$:

```math
U(t)=e^{-iHt}.
```

---

## 14. Single-qubit rotations

Rotations around the Pauli axes are

```math
R_x(\theta)=e^{-i\theta X/2},
```

```math
R_y(\theta)=e^{-i\theta Y/2},
```

```math
R_z(\theta)=e^{-i\theta Z/2}.
```

Since $X^2=I$, the exponential can be evaluated exactly:

```math
e^{-i\theta X/2}
=
\cos\frac\theta2\,I
-i\sin\frac\theta2\,X.
```

Therefore

```math
R_x(\theta)
=
\begin{pmatrix}
\cos(\theta/2)&-i\sin(\theta/2)\\
-i\sin(\theta/2)&\cos(\theta/2)
\end{pmatrix}.
```

Analogous formulas hold for $R_y$ and $R_z$.

These parameterized rotations are fundamental building blocks of parameterized quantum circuits.

---

## 15. Worked example: expectation values of a qubit

Consider

```math
|\psi\rangle
=
\frac{|0\rangle+i|1\rangle}{\sqrt2}.
```

### Expectation of $Z$

```math
\langle Z\rangle
=
\langle\psi|Z|\psi\rangle
=0.
```

### Expectation of $X$

```math
X|\psi\rangle
=
\frac{|1\rangle+i|0\rangle}{\sqrt2},
```

which gives

```math
\langle X\rangle=0.
```

### Expectation of $Y$

The state is the $+1$ eigenstate of $Y$:

```math
Y|\psi\rangle=|\psi\rangle.
```

Therefore

```math
\langle Y\rangle=1.
```

The three expectation values are

```math
(\langle X\rangle,
\langle Y\rangle,
\langle Z\rangle)
=(0,1,0).
```

These are exactly the Cartesian coordinates of the Bloch vector.

---

## 16. Worked example: expanding an observable in the Pauli basis

Let

```math
A=
\begin{pmatrix}
3&1-i\\
1+i&1
\end{pmatrix}.
```

Write

```math
A=a_0I+a_xX+a_yY+a_zZ.
```

Matching entries gives

```math
a_0=2,
\qquad
a_z=1,
\qquad
a_x=1,
\qquad
a_y=1.
```

Therefore

```math
A=2I+X+Y+Z.
```

This decomposition is useful because quantum processors often estimate observables term by term in a Pauli basis.

---

## 17. Common misconceptions

### Misconception 1: "The state vector itself is uniquely physical."

No. Vectors differing only by a global phase represent the same pure physical state.

### Misconception 2: "Any normalized complex vector is a different physical state."

Not if it differs from another vector only by a global phase.

### Misconception 3: "Hermitian and unitary mean the same thing."

No. Hermitian operators represent observables and have real eigenvalues. Unitary operators preserve inner products and represent reversible closed dynamics. Some operators, such as Pauli matrices, happen to be both.

### Misconception 4: "A basis is physically preferred."

The computational basis is operationally convenient, but Hilbert space itself does not privilege it. Other orthonormal bases describe the same state space.

### Misconception 5: "A Hamiltonian is a quantum gate."

A Hamiltonian is a Hermitian generator. A gate can arise from finite-time evolution generated by that Hamiltonian:

```math
U=e^{-iHt}.
```

---

## 18. Connections to later chapters

This chapter provides the mathematical language for:

- [The Bloch Sphere](04-bloch-sphere.md),
- [Composite Systems and Tensor Products](05-composite-systems.md),
- [Measurements and POVMs](08-measurements-and-povms.md),
- [Gate-Based Quantum Computing](../02-quantum-computing/01-gate-model.md),
- [PQC and Ansatz](../05-variational-quantum-algorithms/01-pqc-and-ansatz.md),
- and essentially every quantum-machine-learning model in the repository.

---

## 19. Exercises

### A. Conceptual

1. Why is a Hilbert space defined over complex numbers rather than probabilities alone?
2. Explain the difference between $\langle\phi|\psi\rangle$ and $|\psi\rangle\langle\phi|$.
3. Why does normalization remove one real degree of freedom from a qubit state?
4. Why does global phase remove another real physical degree of freedom?
5. Explain why unitarity implies reversibility.

### B. Computational

6. Normalize the state

```math
|\psi\rangle=2|0\rangle+(1+i)|1\rangle.
```

7. Verify explicitly that $X$, $Y$, and $Z$ are Hermitian and unitary.
8. Compute the eigenvalues and normalized eigenvectors of $X$.
9. Show that

```math
R_z(\theta)
=
\begin{pmatrix}
e^{-i\theta/2}&0\\
0&e^{i\theta/2}
\end{pmatrix}.
```

10. Expand

```math
A=
\begin{pmatrix}
4&2\\
2&0
\end{pmatrix}
```

in the Pauli basis.

11. For

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle,
```

compute $\langle Z\rangle$.

### C. Research-oriented

12. Why are Pauli decompositions particularly useful for near-term variational algorithms?
13. A parameterized circuit can be written as a product of exponentials $e^{-i\theta_jG_j}$. What mathematical properties should the generators $G_j$ have if each factor is to be unitary?
14. Explain why parameter counting alone does not determine the expressive power of a parameterized quantum model.
15. How does the choice of basis affect the apparent sparsity of a state or Hamiltonian without changing the underlying physical system?

---

## 20. Key takeaways

- A finite-dimensional quantum state lives in a complex Hilbert space.
- Pure states are normalized vectors modulo global phase.
- Bras, kets, inner products, and outer products represent distinct mathematical objects.
- Unitary operators preserve inner products and describe reversible closed dynamics.
- Hermitian operators have real spectra and represent observables and Hamiltonians.
- The Pauli matrices form a natural operator basis for one qubit.
- Hermitian Hamiltonians generate unitary evolution through exponentiation.
- A pure qubit has two independent real physical parameters, leading naturally to the Bloch sphere.

---

## References

1. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
2. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
3. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
