# Composite Systems and Tensor Products

## 1. Why composition is where quantum theory becomes genuinely many-body

A single qubit already exhibits superposition and interference, but the most distinctive structure of quantum information appears when systems are combined. Quantum systems compose through the **tensor product**, not through ordinary Cartesian products or by simply listing independent local states.

If system $A$ has Hilbert space $\mathcal H_A$ and system $B$ has Hilbert space $\mathcal H_B$, then the joint system has Hilbert space

```math
\mathcal H_{AB}=\mathcal H_A\otimes\mathcal H_B.
```

This rule produces two crucial consequences:

1. the dimension multiplies,
2. the joint space contains states that cannot be written as products of subsystem states.

The second consequence is entanglement.

### Learning objectives

After this chapter, you should be able to:

- construct tensor-product states and operators,
- compute Kronecker products explicitly,
- distinguish product states from general joint states,
- understand why $n$ qubits span a $2^n$-dimensional space,
- describe local and controlled operations,
- derive Bell-state preparation algebraically,
- compute reduced states using the partial trace,
- and explain why local subsystem descriptions do not determine all joint correlations.

---

## 2. Tensor-product spaces

Let

```math
\dim\mathcal H_A=d_A,
\qquad
\dim\mathcal H_B=d_B.
```

Then

```math
\dim(\mathcal H_A\otimes\mathcal H_B)
=d_Ad_B.
```

For two qubits,

```math
\mathbb C^2\otimes\mathbb C^2
\cong
\mathbb C^4.
```

Using the computational bases of both qubits, the joint basis is

```math
|00\rangle,
\quad
|01\rangle,
\quad
|10\rangle,
\quad
|11\rangle.
```

The notation

```math
|ab\rangle
```

is shorthand for

```math
|a\rangle\otimes|b\rangle.
```

For $n$ qubits,

```math
\mathcal H_n
=(\mathbb C^2)^{\otimes n},
```

and

```math
\dim\mathcal H_n=2^n.
```

---

## 3. Tensor products of vectors

Suppose

```math
|\psi\rangle_A
=
\begin{pmatrix}
\alpha\\
\beta
\end{pmatrix},
```

and

```math
|\phi\rangle_B
=
\begin{pmatrix}
\gamma\\
\delta
\end{pmatrix}.
```

Their tensor product is the Kronecker product

```math
|\psi\rangle_A\otimes|\phi\rangle_B
=
\begin{pmatrix}
\alpha\gamma\\
\alpha\delta\\
\beta\gamma\\
\beta\delta
\end{pmatrix}.
```

In ket notation,

```math
|\psi\rangle_A|\phi\rangle_B
=
\alpha\gamma|00\rangle
+
\alpha\delta|01\rangle
+
\beta\gamma|10\rangle
+
\beta\delta|11\rangle.
```

The tensor product is bilinear:

```math
(a|u\rangle+b|v\rangle)\otimes|w\rangle
=
a|u\rangle\otimes|w\rangle
+b|v\rangle\otimes|w\rangle.
```

This bilinearity is why local superpositions can generate many joint basis amplitudes.

---

## 4. Product states versus general joint states

A general pure two-qubit state is

```math
|\Psi\rangle
=
a|00\rangle
+b|01\rangle
+c|10\rangle
+d|11\rangle,
```

with

```math
|a|^2+|b|^2+|c|^2+|d|^2=1.
```

If it is a product state, then there must exist $\alpha,\beta,\gamma,\delta$ such that

```math
a=\alpha\gamma,
\quad
b=\alpha\delta,
\quad
c=\beta\gamma,
\quad
d=\beta\delta.
```

These coefficients obey

```math
ad=bc.
```

Therefore, for a pure two-qubit state,

```math
ad-bc=0
```

is the product-state condition.

If

```math
ad-bc\neq0,
```

the state is entangled.

For example, the Bell state

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
```

has

```math
a=d=\frac1{\sqrt2},
\qquad
b=c=0,
```

so

```math
ad-bc=\frac12\neq0.
```

It cannot be factorized.

---

## 5. Tensor products of operators

If $A$ acts on subsystem $A$ and $B$ acts on subsystem $B$, their joint action is

```math
A\otimes B.
```

A local operator acting only on the first subsystem is

```math
A\otimes I_B.
```

A local operator acting only on the second subsystem is

```math
I_A\otimes B.
```

The key identity is

```math
(A\otimes B)
(|\psi\rangle\otimes|\phi\rangle)
=
A|\psi\rangle\otimes B|\phi\rangle.
```

Operators acting on distinct subsystems commute:

```math
[A\otimes I,
I\otimes B]=0.
```

This expresses the fact that independent local actions can be applied in either order.

---

## 6. Explicit matrix example

Consider $X$ acting on the first qubit:

```math
X\otimes I.
```

Using

```math
X=
\begin{pmatrix}
0&1\\
1&0
\end{pmatrix},
```

we obtain

```math
X\otimes I
=
\begin{pmatrix}
0&0&1&0\\
0&0&0&1\\
1&0&0&0\\
0&1&0&0
\end{pmatrix}.
```

Its action is

```math
(X\otimes I)|00\rangle=|10\rangle,
```

```math
(X\otimes I)|01\rangle=|11\rangle.
```

Only the first qubit flips.

Similarly,

```math
(I\otimes X)|00\rangle=|01\rangle.
```

---

## 7. Controlled operations

A controlled unitary with the first qubit as control has the form

```math
U_c
=
|0\rangle\langle0|\otimes I
+
|1\rangle\langle1|\otimes U.
```

If the control is $|0\rangle$, nothing happens to the target. If the control is $|1\rangle$, $U$ is applied.

For $U=X$, this becomes CNOT:

```math
\mathrm{CNOT}
=
|0\rangle\langle0|\otimes I
+
|1\rangle\langle1|\otimes X.
```

Its computational-basis action is

```math
|a,b\rangle
\mapsto
|a,b\oplus a\rangle.
```

Controlled gates are central because they couple subsystems and can create entanglement.

---

## 8. Deriving Bell-state preparation

Start with

```math
|00\rangle.
```

Apply a Hadamard gate to the first qubit:

```math
(H\otimes I)|00\rangle
=
H|0\rangle\otimes|0\rangle.
```

Since

```math
H|0\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2},
```

we get

```math
(H\otimes I)|00\rangle
=
\frac{|00\rangle+|10\rangle}{\sqrt2}.
```

Now apply CNOT:

```math
\mathrm{CNOT}
\frac{|00\rangle+|10\rangle}{\sqrt2}
=
\frac{|00\rangle+|11\rangle}{\sqrt2}.
```

Therefore

```math
\mathrm{CNOT}(H\otimes I)|00\rangle
=|\Phi^+\rangle.
```

This derivation shows the two ingredients clearly:

```text
local superposition
→ interaction between subsystems
→ entanglement
```

Neither the Hadamard alone nor CNOT acting on $|00\rangle$ alone creates this Bell state.

---

## 9. Joint density operators

For a product state

```math
\rho_A\otimes\rho_B,
```

all joint information factorizes into the local descriptions.

But a general joint density operator

```math
\rho_{AB}
```

need not factorize.

Even when the global state is pure,

```math
\rho_{AB}
=|\Psi\rangle\langle\Psi|,
```

the local subsystem state may be mixed.

This is where the partial trace becomes necessary.

---

## 10. Partial trace

The reduced state of subsystem $A$ is

```math
\rho_A
=
\mathrm{Tr}_B(\rho_{AB}).
```

If $\{|j\rangle_B\}$ is an orthonormal basis of subsystem $B$, then

```math
\rho_A
=
\sum_j
{}_B\langle j|
\rho_{AB}
|j\rangle_B.
```

The reduced state is defined so that every local expectation value is preserved:

```math
\mathrm{Tr}
\left[
(A\otimes I)\rho_{AB}
\right]
=
\mathrm{Tr}(A\rho_A).
```

Thus $\rho_A$ contains exactly the information needed to predict measurements performed only on subsystem $A$.

---

## 11. Worked example: partial trace of a Bell state

Take

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}.
```

The density matrix is

```math
\rho_{AB}
=
\frac12
\left(
|00\rangle\langle00|
+|00\rangle\langle11|
+|11\rangle\langle00|
+|11\rangle\langle11|
\right).
```

Tracing out $B$ uses

```math
\mathrm{Tr}_B
\left(
|a\rangle|b\rangle
\langle c|\langle d|
\right)
=
\langle d|b\rangle
|a\rangle\langle c|.
```

Therefore the cross terms vanish:

```math
\mathrm{Tr}_B(|00\rangle\langle11|)=0,
```

```math
\mathrm{Tr}_B(|11\rangle\langle00|)=0.
```

The diagonal terms give

```math
\rho_A
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|
=
\frac I2.
```

Similarly,

```math
\rho_B=\frac I2.
```

The joint state is pure, but each local state is maximally mixed.

---

## 12. Local information versus correlation information

For a general two-qubit state, local reduced density matrices do not determine the full joint state.

For example, all four Bell states have

```math
\rho_A=\rho_B=\frac I2,
```

but they are distinct orthogonal joint states.

The information distinguishing them lives in correlations such as

```math
\langle X\otimes X\rangle,
```

```math
\langle Y\otimes Y\rangle,
```

```math
\langle Z\otimes Z\rangle.
```

This is a central lesson for many-body quantum systems: knowing every local state need not determine the global state.

---

## 13. Correlation tensors

A general two-qubit density matrix can be expanded as

```math
\rho_{AB}
=
\frac14
\left[
I\otimes I
+
\sum_i a_i\sigma_i\otimes I
+
\sum_j b_j I\otimes\sigma_j
+
\sum_{i,j}T_{ij}\sigma_i\otimes\sigma_j
\right].
```

The vectors $\mathbf a$ and $\mathbf b$ are local Bloch vectors. The matrix $T$ contains two-body correlations:

```math
T_{ij}
=
\mathrm{Tr}
\left[
\rho_{AB}
(\sigma_i\otimes\sigma_j)
\right].
```

This decomposition makes explicit why two local Bloch vectors are insufficient: the correlation tensor carries additional joint information.

---

## 14. Dimension growth and its interpretation

For $n$ qubits,

```math
\dim\mathcal H_n=2^n.
```

A general pure state is

```math
|\psi\rangle
=
\sum_{x\in\{0,1\}^n}
\alpha_x|x\rangle.
```

The number of amplitudes grows exponentially. This makes direct classical state-vector simulation expensive for arbitrary states.

However, two warnings are essential:

1. many physically relevant states have additional structure and may admit compressed classical descriptions,
2. measurement does not provide direct access to all amplitudes.

Therefore exponential Hilbert-space dimension is a statement about representation space, not automatically about computational speedup.

---

## 15. Locality

Many realistic Hamiltonians are sums of terms acting on only a few subsystems:

```math
H
=
\sum_j H_j.
```

A $k$-local Hamiltonian has terms that each act on at most $k$ subsystems.

For example,

```math
H
=
\sum_i h_iZ_i
+
\sum_{(i,j)}J_{ij}Z_iZ_j.
```

Locality matters because it affects:

- experimental implementability,
- circuit depth,
- entanglement growth,
- tensor-network simulability,
- Lieb-Robinson-type propagation constraints,
- variational ansatz design,
- and QML trainability.

The geometry of interactions can matter as much as the total Hilbert-space dimension.

---

## 16. Worked example: is a two-qubit state a product?

Consider

```math
|\psi\rangle
=
\frac12
\left(
|00\rangle
+|01\rangle
+|10\rangle
+|11\rangle
\right).
```

Here

```math
a=b=c=d=\frac12.
```

Then

```math
ad-bc
=
\frac14-\frac14
=0.
```

So the state is a product state. Indeed,

```math
|\psi\rangle
=
|+\rangle\otimes|+\rangle.
```

Now consider

```math
|\phi\rangle
=
\frac{|00\rangle+|01\rangle+|10\rangle-|11\rangle}{2}.
```

Then

```math
ad-bc
=
-\frac14-\frac14
=-\frac12.
```

Therefore $|\phi\rangle$ is entangled.

---

## 17. Common misconceptions

### Misconception 1: "A two-qubit state is always two individual qubit states written together."

False. Entangled states do not admit such a factorization.

### Misconception 2: "The tensor product is just notation."

No. It is the composition rule that determines the joint state space and permits entanglement.

### Misconception 3: "If the global state is pure, each subsystem must also be pure."

False. A subsystem of an entangled pure state can be mixed.

### Misconception 4: "Knowing both local density matrices determines the global state."

False. Joint correlations can contain additional information.

### Misconception 5: "Exponential Hilbert-space dimension means exponential readable memory."

False. The state space is exponentially large, but accessible classical information is constrained by measurement.

---

## 18. Connections to later chapters

This chapter is the bridge to:

- [Entanglement](06-entanglement.md),
- [Density Matrices and Mixed States](07-density-matrices.md),
- [Quantum Channels](../06-quantum-information-theory/01-quantum-channels.md),
- [Entanglement Theory](../06-quantum-information-theory/03-entanglement-theory.md),
- multiqubit gates and circuits,
- quantum simulation,
- and structured quantum-machine-learning architectures.

---

## 19. Exercises

### A. Conceptual

1. Why do Hilbert-space dimensions multiply when quantum systems are combined?
2. What information can be lost when replacing $\rho_{AB}$ by $\rho_A$ and $\rho_B$?
3. Why do operators acting on different subsystems commute?
4. Explain why CNOT is capable of creating entanglement but does not entangle every input state.
5. Why is local information insufficient to characterize a general many-body state?

### B. Computational

6. Compute

```math
|+\rangle\otimes|-\rangle
```

in the computational basis.

7. Construct the $4\times4$ matrix of $Z\otimes X$.
8. Determine whether

```math
|\psi\rangle
=
\frac{1}{\sqrt3}
\left(
|00\rangle+|01\rangle+|11\rangle
\right)
```

is a product state.

9. Compute the reduced density matrix of subsystem $A$ for

```math
|\psi\rangle
=
\sqrt{p}|00\rangle
+
\sqrt{1-p}|11\rangle.
```

10. For the Bell state $|\Phi^+\rangle$, compute

```math
\langle X\otimes X\rangle
```

and

```math
\langle Z\otimes Z\rangle.
```

### C. Research-oriented

11. Explain why local observables can fail to distinguish globally different quantum states.
12. How can locality make an exponentially large many-body Hilbert space classically tractable in special cases?
13. Why might a QML architecture that uses only local measurements miss useful global correlations?
14. Compare the resources "number of qubits" and "interaction graph connectivity." Why can the second matter strongly even at fixed qubit count?

---

## 20. Key takeaways

- Quantum systems compose by tensor products.
- Dimensions multiply, giving an exponentially growing many-qubit state space.
- Product states occupy only a restricted subset of the joint state space.
- Controlled interactions can transform local superposition into entanglement.
- Reduced density matrices describe local measurement statistics but discard some joint information.
- Correlation tensors contain information not visible in local Bloch vectors.
- Exponential dimension alone does not establish computational advantage.
- Locality is a structural resource and constraint throughout quantum computing and QML.

---

## References

1. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
2. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
3. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
