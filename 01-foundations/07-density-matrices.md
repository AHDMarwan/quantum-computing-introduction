# Density Matrices and Mixed States

## 1. Why state vectors are not enough

A ket $|\psi\rangle$ describes a pure quantum state. That is sufficient only when the system is known to be in a definite pure state and is treated as closed.

Quantum information routinely requires a more general description because we may have:

- classical uncertainty over several possible preparations,
- a subsystem of an entangled state,
- interaction with an environment,
- noisy preparation or evolution,
- incomplete information about a source,
- or a learning protocol that receives an ensemble rather than a single pure state.

The correct general state representation is the **density operator**.

### Learning objectives

After this chapter, you should be able to:

- construct density operators from statistical ensembles,
- state and use the validity conditions for density matrices,
- distinguish pure and mixed states using purity and eigenvalues,
- explain why ensemble decompositions are not unique,
- compute expectation values with the trace rule,
- compute reduced density matrices,
- use the Bloch representation of one-qubit mixed states,
- interpret unitary and noisy state evolution,
- and work with basic state-distance and fidelity notions.

---

## 2. From an ensemble to a density operator

Suppose a preparation procedure produces $|\psi_j\rangle$ with classical probability $p_j$, where

```math
p_j\ge0,
\qquad
\sum_jp_j=1.
```

The ensemble is written

```math
\{p_j,|\psi_j\rangle\}_j.
```

Its density operator is

```math
\rho
=
\sum_j
p_j
|\psi_j\rangle\langle\psi_j|.
```

The density operator combines quantum amplitudes inside each pure-state projector with classical uncertainty across preparations.

---

## 3. Conditions for a valid density operator

A matrix $\rho$ represents a physical quantum state if and only if

```math
\rho\succeq0
```

and

```math
\mathrm{Tr}(\rho)=1.
```

Positivity means

```math
\langle\phi|\rho|\phi\rangle\ge0
```

for every $|\phi\rangle$.

Since positive semidefinite operators are Hermitian, a density operator has real nonnegative eigenvalues.

If

```math
\rho
=
\sum_k\lambda_k|k\rangle\langle k|,
```

then

```math
\lambda_k\ge0,
\qquad
\sum_k\lambda_k=1.
```

Thus the eigenvalues themselves form a probability distribution.

---

## 4. Pure states as a special case

A pure state has

```math
\rho
=
|\psi\rangle\langle\psi|.
```

Then

```math
\rho^2
=
|\psi\rangle\langle\psi|\psi\rangle\langle\psi|
=
\rho,
```

because

```math
\langle\psi|\psi\rangle=1.
```

Therefore a pure-state density matrix is a rank-one projector.

Its eigenvalues are

```math
1,0,0,\ldots
```

and its rank is one.

---

## 5. Purity

The quantity

```math
\gamma(\rho)
=
\mathrm{Tr}(\rho^2)
```

is called the **purity**.

If the eigenvalues of $\rho$ are $\lambda_k$, then

```math
\mathrm{Tr}(\rho^2)
=
\sum_k\lambda_k^2.
```

For a pure state,

```math
\mathrm{Tr}(\rho^2)=1.
```

For a mixed state,

```math
\mathrm{Tr}(\rho^2)<1.
```

In a $d$-dimensional Hilbert space, the maximally mixed state is

```math
\rho_*
=
\frac{I_d}{d}.
```

Its purity is

```math
\mathrm{Tr}(\rho_*^2)
=
\frac1d.
```

Therefore

```math
\frac1d
\le
\mathrm{Tr}(\rho^2)
\le
1.
```

---

## 6. Mixed states are not merely noisy pure states

A mixed state is not defined by "having experimental noise." It is defined mathematically by the density operator not being rank one.

A subsystem of a perfectly pure entangled state can be mixed even when the global system is noiseless.

For example,

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
```

is pure, but

```math
\rho_A
=
\mathrm{Tr}_B
(|\Phi^+\rangle\langle\Phi^+|)
=
\frac I2.
```

This local mixedness comes from entanglement, not classical ignorance about a secretly definite local pure state.

---

## 7. Ensemble decompositions are not unique

The same density operator can arise from different preparation ensembles.

For example,

```math
\frac I2
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|.
```

But also

```math
\frac I2
=
\frac12|+\rangle\langle+|
+
\frac12|-\rangle\langle-|.
```

And also

```math
\frac I2
=
\frac12|+i\rangle\langle+i|
+
\frac12|-i\rangle\langle-i|.
```

No measurement on the system alone can determine which of these ensemble decompositions was "really used" if the density operator is the same.

Operational predictions depend on $\rho$, not on a preferred decomposition.

This nonuniqueness is a major conceptual difference between a density operator and a classical list of hidden pure states.

---

## 8. Expectation values

For an observable $A$, the expectation value in state $\rho$ is

```math
\langle A\rangle_\rho
=
\mathrm{Tr}(\rho A).
```

For a pure state

```math
\rho=|\psi\rangle\langle\psi|,
```

we recover

```math
\mathrm{Tr}(\rho A)
=
\langle\psi|A|\psi\rangle.
```

For an ensemble,

```math
\rho
=
\sum_jp_j|\psi_j\rangle\langle\psi_j|,
```

we obtain

```math
\mathrm{Tr}(\rho A)
=
\sum_jp_j
\langle\psi_j|A|\psi_j\rangle.
```

Thus the trace rule automatically averages both quantum and classical uncertainty.

---

## 9. One-qubit density matrices

Any one-qubit density operator can be written

```math
\rho
=
\frac12
\left(
I+\mathbf r\cdot\boldsymbol\sigma
\right).
```

Explicitly,

```math
\rho
=
\frac12
\begin{pmatrix}
1+r_z&r_x-ir_y\\
r_x+ir_y&1-r_z
\end{pmatrix}.
```

The Bloch vector satisfies

```math
\|\mathbf r\|\le1.
```

The purity is

```math
\mathrm{Tr}(\rho^2)
=
\frac12
\left(
1+\|\mathbf r\|^2
\right).
```

Therefore:

```text
|r| = 1  → pure qubit
|r| < 1  → mixed qubit
|r| = 0  → maximally mixed qubit
```

---

## 10. Convexity of quantum state space

If $\rho_1$ and $\rho_2$ are valid states and

```math
0\le p\le1,
```

then

```math
\rho
=
p\rho_1+(1-p)\rho_2
```

is also a valid state.

Thus the set of density operators is convex.

Pure states are extreme points of this convex set: a pure state cannot be written as a nontrivial convex mixture of two different density operators.

For a qubit, this convex geometry is exactly the Bloch ball.

---

## 11. Reduced density operators

Given a joint state $\rho_{AB}$, the state available to subsystem $A$ is

```math
\rho_A
=
\mathrm{Tr}_B(\rho_{AB}).
```

The partial trace is defined so that every local expectation value is preserved:

```math
\mathrm{Tr}
\left[
(A\otimes I)\rho_{AB}
\right]
=
\mathrm{Tr}(A\rho_A).
```

Therefore $\rho_A$ contains all information needed for measurements performed only on subsystem $A$.

It does not, in general, contain all information about correlations with $B$.

---

## 12. Worked example: reduced state of a partially entangled pair

Consider

```math
|\psi\rangle
=
\sqrt p|00\rangle
+
\sqrt{1-p}|11\rangle.
```

The joint density operator is

```math
\rho_{AB}
=
p|00\rangle\langle00|
+
\sqrt{p(1-p)}|00\rangle\langle11|
+
\sqrt{p(1-p)}|11\rangle\langle00|
+
(1-p)|11\rangle\langle11|.
```

Tracing out $B$ removes the cross terms:

```math
\rho_A
=
p|0\rangle\langle0|
+
(1-p)|1\rangle\langle1|.
```

Its purity is

```math
\mathrm{Tr}(\rho_A^2)
=
p^2+(1-p)^2.
```

At $p=1/2$,

```math
\mathrm{Tr}(\rho_A^2)=\frac12,
```

so the local qubit is maximally mixed.

At $p=0$ or $p=1$,

```math
\mathrm{Tr}(\rho_A^2)=1,
```

because the global state becomes a product state.

---

## 13. Spectral decomposition of a density operator

Because $\rho$ is Hermitian and positive,

```math
\rho
=
\sum_k\lambda_k|k\rangle\langle k|,
```

with

```math
\lambda_k\ge0,
\qquad
\sum_k\lambda_k=1.
```

This decomposition resembles an ensemble, but it has a special feature: the eigenvectors are orthogonal.

The spectral decomposition is useful for computing:

- von Neumann entropy,
- purity,
- functions of density operators,
- distinguishability measures,
- and entanglement spectra.

---

## 14. Von Neumann entropy preview

The von Neumann entropy is

```math
S(\rho)
=
-\mathrm{Tr}(\rho\log_2\rho).
```

Using the eigenvalues,

```math
S(\rho)
=
-\sum_k\lambda_k\log_2\lambda_k.
```

For a pure state,

```math
S(\rho)=0.
```

For the maximally mixed state in dimension $d$,

```math
S\left(\frac{I_d}{d}\right)
=
\log_2d.
```

Entropy is developed systematically in [Entropy and Information](../06-quantum-information-theory/02-entropy-and-information.md).

---

## 15. Unitary evolution in density-matrix form

If a pure state evolves as

```math
|\psi\rangle
\mapsto
U|\psi\rangle,
```

then

```math
\rho
=|\psi\rangle\langle\psi|
```

evolves as

```math
\rho
\mapsto
U\rho U^\dagger.
```

This formula also applies to mixed states.

Unitary evolution preserves the eigenvalues of $\rho$, and therefore preserves purity and von Neumann entropy.

It can rotate a state in Hilbert space, but it cannot turn a mixed state into a pure state without access to additional systems or postselection.

---

## 16. General noisy evolution

The most general deterministic physical evolution of a quantum state is described by a completely positive trace-preserving map, or quantum channel:

```math
\rho
\mapsto
\mathcal E(\rho).
```

A Kraus representation is

```math
\mathcal E(\rho)
=
\sum_k
K_k\rho K_k^\dagger,
```

with

```math
\sum_kK_k^\dagger K_k=I.
```

The completeness condition ensures trace preservation.

Quantum channels are developed in detail in [Quantum Channels](../06-quantum-information-theory/01-quantum-channels.md).

---

## 17. Worked example: dephasing destroys coherence

Consider

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2},
```

with

```math
\rho_+
=
\frac12
\begin{pmatrix}
1&1\\
1&1
\end{pmatrix}.
```

A complete dephasing channel in the computational basis removes the off-diagonal terms:

```math
\Delta(\rho)
=
|0\rangle\langle0|\rho|0\rangle\langle0|
+
|1\rangle\langle1|\rho|1\rangle\langle1|.
```

Therefore

```math
\Delta(\rho_+)
=
\frac12
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix}
=
\frac I2.
```

The computational-basis populations remain unchanged, but phase coherence is lost.

This is the density-matrix expression of decoherence.

---

## 18. Trace distance

The trace distance between states $\rho$ and $\sigma$ is

```math
D(\rho,\sigma)
=
\frac12
\|\rho-\sigma\|_1,
```

where

```math
\|A\|_1
=
\mathrm{Tr}\sqrt{A^\dagger A}.
```

Trace distance has an operational interpretation in state distinguishability. It ranges from

```math
0\le D(\rho,\sigma)\le1.
```

If

```math
D(\rho,\sigma)=0,
```

the states are identical.

If

```math
D(\rho,\sigma)=1,
```

they are perfectly distinguishable.

---

## 19. Fidelity

A common fidelity convention is

```math
F(\rho,\sigma)
=
\left[
\mathrm{Tr}
\sqrt{
\sqrt\rho\,\sigma\sqrt\rho
}
\right]^2.
```

If one state is pure,

```math
\rho=|\psi\rangle\langle\psi|,
```

then

```math
F(|\psi\rangle,\sigma)
=
\langle\psi|\sigma|\psi\rangle.
```

Fidelity quantifies similarity, while trace distance quantifies distinguishability.

Both appear in state preparation, verification, error correction, tomography, and quantum machine learning.

---

## 20. Worked example: two ensembles, one state

Take ensemble A:

```math
\left\{
\frac12,|0\rangle;
\frac12,|1\rangle
\right\}.
```

Then

```math
\rho_A
=
\frac12
\begin{pmatrix}
1&0\\
0&0
\end{pmatrix}
+
\frac12
\begin{pmatrix}
0&0\\
0&1
\end{pmatrix}
=
\frac I2.
```

Take ensemble B:

```math
\left\{
\frac12,|+\rangle;
\frac12,|-\rangle
\right\}.
```

Now

```math
|+\rangle\langle+|
=
\frac12
\begin{pmatrix}
1&1\\
1&1
\end{pmatrix},
```

and

```math
|-\rangle\langle-|
=
\frac12
\begin{pmatrix}
1&-1\\
-1&1
\end{pmatrix}.
```

Averaging gives

```math
\rho_B
=
\frac I2.
```

No experiment on the system alone can distinguish ensemble A from ensemble B once the preparation label is discarded.

---

## 21. Common misconceptions

### Misconception 1: "A mixed state means the experiment is badly prepared."

No. Mixedness can arise fundamentally from tracing out part of an entangled pure state.

### Misconception 2: "The density matrix tells us which pure state the system is secretly in."

No. Density matrices generally have many ensemble decompositions with identical operational predictions.

### Misconception 3: "Off-diagonal entries always mean entanglement."

No. Off-diagonal entries depend on basis and can represent single-system coherence. Entanglement is a property of composite-state separability.

### Misconception 4: "A unitary can purify a mixed state."

Not on the same closed system. Unitaries preserve the spectrum of $\rho$.

### Misconception 5: "Purity and fidelity are the same quantity."

No. Purity measures how mixed one state is; fidelity compares two states.

---

## 22. Connections to later chapters

Density operators are the default language for:

- [Measurements and POVMs](08-measurements-and-povms.md),
- [Quantum Channels](../06-quantum-information-theory/01-quantum-channels.md),
- [Entropy and Information](../06-quantum-information-theory/02-entropy-and-information.md),
- [Entanglement Theory](../06-quantum-information-theory/03-entanglement-theory.md),
- noisy variational algorithms,
- quantum state learning,
- and learning directly from quantum data.

---

## 23. Exercises

### A. Conceptual

1. Why is a density operator more general than a state vector?
2. Explain why ensemble decomposition is not unique.
3. Why can a subsystem of a pure state be mixed?
4. Why does unitary evolution preserve purity?
5. What is the operational difference between trace distance and fidelity?

### B. Computational

6. Determine whether

```math
\rho
=
\begin{pmatrix}
0.7&0.2\\
0.2&0.3
\end{pmatrix}
```

is a valid density matrix.

7. Compute its purity.
8. Find the Bloch vector of

```math
\rho
=
\frac12
\begin{pmatrix}
1&-i/2\\
i/2&1
\end{pmatrix}.
```

9. Compute the reduced state of the first qubit for

```math
|\psi\rangle
=
\frac{|00\rangle+|01\rangle+|10\rangle-|11\rangle}{2}.
```

10. Apply complete dephasing to

```math
\rho
=
\begin{pmatrix}
3/4&1/4\\
1/4&1/4
\end{pmatrix}.
```

11. Compute the trace distance between $|0\rangle\langle0|$ and $|1\rangle\langle1|$.

### C. Research-oriented

12. In QML, when would a density-matrix model be more natural than a pure-state model?
13. Why can noise sometimes be modeled as loss of off-diagonal coherence in one basis but not in every basis simultaneously?
14. How could two learning datasets correspond to different ensembles but the same density operator? What information would then be inaccessible to any learner receiving only the quantum states?
15. Why should trainability analyses of noisy parameterized circuits often be expressed in the density-matrix or channel formalism rather than only with state vectors?

---

## 24. Key takeaways

- Density operators describe all finite-dimensional quantum states, pure or mixed.
- Valid states are positive semidefinite and have unit trace.
- Pure states are rank-one projectors with unit purity.
- Mixed-state ensemble decompositions are generally nonunique.
- Expectation values are computed with $\mathrm{Tr}(\rho A)$.
- Reduced states arise from the partial trace.
- Unitary evolution preserves the spectrum of $\rho$.
- General open-system dynamics require quantum channels.
- Trace distance and fidelity quantify distinguishability and similarity.

---

## References

1. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
2. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
3. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
