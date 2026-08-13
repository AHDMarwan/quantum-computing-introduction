# Composite Systems and Tensor Products

## 1. Building larger quantum systems

If system \(A\) has Hilbert space \(\mathcal H_A\) and system \(B\) has Hilbert space \(\mathcal H_B\), the joint system is described by

\[
\mathcal H_{AB}=\mathcal H_A\otimes\mathcal H_B.
\]

For two qubits,

\[
\mathcal H_{AB}=\mathbb C^2\otimes\mathbb C^2\cong\mathbb C^4.
\]

A standard basis is

\[
|00\rangle,\ |01\rangle,\ |10\rangle,\ |11\rangle.
\]

For \(n\) qubits,

\[
\mathcal H_n=(\mathbb C^2)^{\otimes n},
\qquad
\dim\mathcal H_n=2^n.
\]

## 2. Product states

If

\[
|\psi\rangle_A=\alpha|0\rangle+\beta|1\rangle,
\]

and

\[
|\phi\rangle_B=\gamma|0\rangle+\delta|1\rangle,
\]

then

\[
|\psi\rangle_A\otimes|\phi\rangle_B
=
\alpha\gamma|00\rangle
+\alpha\delta|01\rangle
+\beta\gamma|10\rangle
+\beta\delta|11\rangle.
\]

States that can be written this way are product states. States that cannot are entangled.

## 3. Operators on subsystems

An operator acting only on subsystem \(A\) is represented on the joint space as

\[
A\otimes I_B.
\]

Similarly, an operation on \(B\) is

\[
I_A\otimes B.
\]

Operators on distinct subsystems commute:

\[
[A\otimes I, I\otimes B]=0.
\]

This simple rule is used constantly in circuit notation and Hamiltonian construction.

## 4. Controlled operations

A controlled unitary has the form

\[
U_c
=
|0\rangle\langle0|\otimes I
+
|1\rangle\langle1|\otimes U.
\]

The CNOT gate is the special case \(U=X\):

\[
\operatorname{CNOT}|a,b\rangle
=
|a,b\oplus a\rangle.
\]

Applied to

\[
|+\rangle|0\rangle,
\]

it produces

\[
\frac{|00\rangle+|11\rangle}{\sqrt2},
\]

a Bell state. This demonstrates how local superposition plus an entangling interaction creates non-product correlations.

## 5. Partial trace

A joint density operator \(\rho_{AB}\) determines the local state of subsystem \(A\) through the partial trace:

\[
\rho_A=\operatorname{Tr}_B(\rho_{AB}).
\]

The partial trace is defined so that expectation values of local observables are preserved:

\[
\operatorname{Tr}\big[(A\otimes I)\rho_{AB}\big]
=
\operatorname{Tr}(A\rho_A).
\]

This operation is essential because subsystems of a pure entangled state can be mixed.

## 6. Dimension and computational representation

The dimension \(2^n\) explains why direct classical state-vector simulation becomes expensive as \(n\) grows. However, the state vector is not a random-access classical memory containing \(2^n\) readable numbers. Quantum algorithms manipulate the vector coherently and obtain restricted measurement outcomes.

This distinction is central when discussing claims that quantum machine learning obtains an advantage simply because it uses an exponentially large Hilbert space.

## 7. Locality

Many physical Hamiltonians and quantum circuits are built from local terms, for example

\[
H=\sum_{(i,j)} H_{ij},
\]

where each \(H_{ij}\) acts on only a small number of subsystems. Locality strongly affects simulation cost, entanglement growth, circuit depth, trainability, and the structure of useful ansätze.

## 8. Key takeaway

Tensor products are not optional notation: they are the rule that determines how quantum systems compose. They create an exponentially growing joint state space and permit states that cannot be factorized into independent subsystems. That nonfactorizability is entanglement.

## References

1. J. Watrous, *The Theory of Quantum Information*: https://cs.uwaterloo.ca/~watrous/TQI/
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
