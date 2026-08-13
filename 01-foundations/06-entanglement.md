# Entanglement

## 1. Why entanglement matters

Entanglement is the failure of a composite quantum state to decompose into independent subsystem states. It is one of the central structural features of quantum information, but it is often described too loosely.

Entanglement is not the same as:

- ordinary correlation,
- superposition,
- nonlocality,
- computational speedup,
- or "having many qubits."

It is a precise statement about the tensor-product structure of a quantum state.

### Learning objectives

After this chapter, you should be able to:

- test whether a pure bipartite state is separable,
- derive and interpret the Schmidt decomposition,
- compute reduced density matrices of pure bipartite states,
- connect Schmidt coefficients to entanglement entropy,
- distinguish entanglement from classical correlation,
- state the definition of mixed-state separability,
- distinguish entanglement from Bell nonlocality,
- and explain how entanglement should be treated as a resource rather than as an automatic certificate of quantum advantage.

---

## 2. Pure-state separability

A bipartite pure state $|\psi\rangle_{AB}$ is **separable** if there exist normalized states $|a\rangle_A$ and $|b\rangle_B$ such that

```math
|\psi\rangle_{AB}
=
|a\rangle_A\otimes|b\rangle_B.
```

If no such factorization exists, the state is entangled.

The canonical example is

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}.
```

This state cannot be written as a tensor product of one-qubit states.

---

## 3. A direct separability test for two pure qubits

Write a general two-qubit pure state as

```math
|\psi\rangle
=
a|00\rangle
+b|01\rangle
+c|10\rangle
+d|11\rangle.
```

Associate the coefficient matrix

```math
C=
\begin{pmatrix}
a&b\\
c&d
\end{pmatrix}.
```

The state is a product state exactly when $C$ has rank one. For a $2\times2$ matrix, this means

```math
\det C=ad-bc=0.
```

Therefore

```math
ad-bc\neq0
```

implies entanglement.

For the Bell state,

```math
C=
\frac1{\sqrt2}
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix},
```

so

```math
\det C=\frac12\neq0.
```

---

## 4. Reduced states reveal pure-state entanglement

For

```math
\rho_{AB}
=|\psi\rangle\langle\psi|,
```

the reduced state of $A$ is

```math
\rho_A
=
\mathrm{Tr}_B(\rho_{AB}).
```

If $|\psi\rangle_{AB}$ is a product state,

```math
|\psi\rangle_{AB}
=|a\rangle_A|b\rangle_B,
```

then

```math
\rho_A=|a\rangle\langle a|,
```

which is pure.

Conversely, for a bipartite pure state, if $\rho_A$ is mixed, then the global state is entangled.

For the Bell state,

```math
\rho_A
=
\rho_B
=
\frac I2.
```

The global state is pure while each subsystem is maximally mixed.

---

## 5. Schmidt decomposition

Every bipartite pure state can be written as

```math
|\psi\rangle_{AB}
=
\sum_{k=1}^{r}
\sqrt{\lambda_k}
|u_k\rangle_A
|v_k\rangle_B,
```

where

```math
\lambda_k\ge0,
\qquad
\sum_k\lambda_k=1,
```

and $\{|u_k\rangle_A\}$ and $\{|v_k\rangle_B\}$ are orthonormal sets.

The integer $r$ is the **Schmidt rank**.

A pure bipartite state is separable if and only if

```math
r=1.
```

If

```math
r>1,
```

the state is entangled.

---

## 6. Where Schmidt decomposition comes from

Choose product bases $\{|i\rangle_A\}$ and $\{|j\rangle_B\}$. Write

```math
|\psi\rangle
=
\sum_{i,j}C_{ij}|i\rangle_A|j\rangle_B.
```

The coefficient array $C$ is a matrix. Perform a singular-value decomposition:

```math
C=U\Sigma V^\dagger.
```

Let the singular values be

```math
s_k\ge0.
```

Absorbing the unitary basis changes into new orthonormal states $|u_k\rangle_A$ and $|v_k\rangle_B$ gives

```math
|\psi\rangle
=
\sum_k s_k
|u_k\rangle_A|v_k\rangle_B.
```

Normalization requires

```math
\sum_k s_k^2=1.
```

Defining

```math
\lambda_k=s_k^2
```

gives the Schmidt form.

Thus Schmidt decomposition is the singular-value decomposition of the bipartite amplitude matrix.

---

## 7. Reduced states from Schmidt coefficients

Starting from

```math
|\psi\rangle
=
\sum_k\sqrt{\lambda_k}
|u_k\rangle_A|v_k\rangle_B,
```

we have

```math
\rho_{AB}
=
\sum_{k,\ell}
\sqrt{\lambda_k\lambda_\ell}
|u_k\rangle\langle u_\ell|
\otimes
|v_k\rangle\langle v_\ell|.
```

Tracing out $B$ gives

```math
\rho_A
=
\sum_k
\lambda_k
|u_k\rangle\langle u_k|.
```

Similarly,

```math
\rho_B
=
\sum_k
\lambda_k
|v_k\rangle\langle v_k|.
```

Therefore the two reduced density matrices have the same nonzero eigenvalues $\lambda_k$.

This is why pure-state entanglement can be quantified by the spectrum of either reduced state.

---

## 8. Entanglement entropy

For a bipartite pure state, the entanglement entropy is the von Neumann entropy of either reduced state:

```math
E(|\psi\rangle)
=
S(\rho_A)
=
S(\rho_B).
```

Using the Schmidt coefficients,

```math
E(|\psi\rangle)
=
-\sum_k
\lambda_k\log_2\lambda_k.
```

For a product state,

```math
\lambda_1=1,
```

so

```math
E=0.
```

For a Bell state,

```math
\lambda_1=\lambda_2=\frac12,
```

and therefore

```math
E=1
```

bit of entanglement entropy.

---

## 9. A continuously tunable two-qubit example

Consider

```math
|\psi(p)\rangle
=
\sqrt p|00\rangle
+
\sqrt{1-p}|11\rangle,
```

where

```math
0\le p\le1.
```

This state is already in Schmidt form, with

```math
\lambda_1=p,
\qquad
\lambda_2=1-p.
```

The reduced state is

```math
\rho_A
=
p|0\rangle\langle0|
+(1-p)|1\rangle\langle1|.
```

The entanglement entropy is

```math
E(p)
=
-p\log_2p
-(1-p)\log_2(1-p).
```

It vanishes at

```math
p=0
\quad\text{and}\quad
p=1,
```

where the state is a product state, and is maximal at

```math
p=\frac12.
```

This example shows that entanglement is quantitative, not merely binary.

---

## 10. Correlation is not entanglement

Consider the mixed state

```math
\rho_{\mathrm{cc}}
=
\frac12|00\rangle\langle00|
+
\frac12|11\rangle\langle11|.
```

Measurements in the computational basis are perfectly correlated: the outcomes are always equal.

Yet the state is separable because it is explicitly a convex mixture of product states.

Thus

```math
\text{correlation}
\not\Rightarrow
\text{entanglement}.
```

The Bell state

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
```

and the classical mixture $\rho_{\mathrm{cc}}$ have identical $Z$-basis populations but differ in their coherence and correlations in other bases.

For example,

```math
\langle X\otimes X\rangle_{|\Phi^+\rangle}=1,
```

while

```math
\langle X\otimes X\rangle_{\rho_{\mathrm{cc}}}=0.
```

---

## 11. Mixed-state separability

A bipartite mixed state is separable if it can be written as

```math
\rho_{AB}
=
\sum_j
p_j
\rho_A^{(j)}
\otimes
\rho_B^{(j)},
```

with

```math
p_j\ge0,
\qquad
\sum_jp_j=1.
```

If no such convex decomposition exists, the state is entangled.

Pure-state separability reduces to a simple factorization problem. Mixed-state separability is substantially harder because one must reason over all possible convex decompositions.

For low-dimensional bipartite systems, the positive-partial-transpose criterion is especially useful, but a full treatment belongs in [Entanglement Theory](../06-quantum-information-theory/03-entanglement-theory.md).

---

## 12. Entanglement versus Bell nonlocality

Bell nonlocality concerns whether observed correlations can be reproduced by a local hidden-variable model.

Entanglement concerns whether a quantum state is separable.

These are related but distinct concepts.

For general mixed states,

```math
\text{Bell-nonlocal}
\Rightarrow
\text{entangled},
```

but

```math
\text{entangled}
\not\Rightarrow
\text{Bell-nonlocal under every standard test}.
```

Some entangled mixed states do not violate a given Bell inequality for a given measurement scenario.

Therefore

```math
\text{entanglement}
\neq
\text{Bell nonlocality}.
```

---

## 13. CHSH as an operational example

In a CHSH experiment, Alice chooses between observables $A_0,A_1$ and Bob between $B_0,B_1$, each with outcomes $\pm1$.

Define

```math
S
=
\langle A_0B_0\rangle
+
\langle A_0B_1\rangle
+
\langle A_1B_0\rangle
-
\langle A_1B_1\rangle.
```

Local hidden-variable models satisfy

```math
|S|\le2.
```

Quantum mechanics permits

```math
|S|\le2\sqrt2.
```

A suitable Bell state and measurement choices reach the quantum maximum.

The point is not that every entangled state automatically reaches $2\sqrt2$, but that entanglement can support correlations outside the local classical polytope.

---

## 14. Entanglement as a resource

In a resource-theoretic viewpoint, entanglement is useful only relative to:

- a specified task,
- a set of allowed operations,
- a cost model,
- and a resource measure.

For example, entanglement is a resource in:

- quantum teleportation,
- superdense coding,
- entanglement-assisted communication,
- distributed quantum protocols,
- some metrological settings,
- and many-body state preparation.

But the statement

> "the circuit creates entanglement"

is much weaker than

> "the circuit achieves a provable advantage because a quantified entanglement resource enables a task that the restricted competitor cannot perform efficiently."

---

## 15. Entanglement and classical simulability

Entanglement can make classical simulation difficult, but the relationship is not one-to-one.

Some entangled states admit efficient classical descriptions because of additional structure. Tensor-network methods exploit restricted entanglement patterns, and stabilizer circuits can generate highly nontrivial entangled states while remaining efficiently classically simulable under the Gottesman-Knill setting.

Therefore

```math
\text{entangled}
\not\Rightarrow
\text{classically hard}.
```

Conversely, when entanglement grows broadly across a system, many compressed classical representations become more expensive. The relevant question is the structure and amount of entanglement, not merely whether it is nonzero.

---

## 16. Entanglement in variational circuits and QML

In parameterized quantum models, entangling gates can increase the range of correlations and functions that a circuit can represent.

However, increasing entanglement indiscriminately is not a universal design principle. Highly expressive or random-like circuits can become difficult to train, and strong entanglement can coexist with classical simulability in structured cases.

A careful QML analysis should distinguish:

```text
entanglement generation
≠ expressivity
≠ trainability
≠ generalization
≠ quantum advantage
```

These quantities can interact, but none is an automatic substitute for another.

---

## 17. Worked example: Schmidt decomposition of a simple state

Consider

```math
|\psi\rangle
=
\frac{\sqrt3}{2}|00\rangle
+
\frac12|11\rangle.
```

This is already in Schmidt form:

```math
\lambda_1=\frac34,
\qquad
\lambda_2=\frac14.
```

The reduced state is

```math
\rho_A
=
\frac34|0\rangle\langle0|
+
\frac14|1\rangle\langle1|.
```

The entanglement entropy is

```math
E
=
-\frac34\log_2\frac34
-\frac14\log_2\frac14.
```

Since both Schmidt coefficients are nonzero, the state is entangled, but not maximally entangled.

---

## 18. Worked example: same local states, different global states

Compare

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
```

and

```math
|\Phi^-\rangle
=
\frac{|00\rangle-|11\rangle}{\sqrt2}.
```

For both states,

```math
\rho_A=\rho_B=\frac I2.
```

Thus no measurement on only one subsystem can distinguish the two states.

However,

```math
\langle X\otimes X\rangle_{\Phi^+}=1,
```

while

```math
\langle X\otimes X\rangle_{\Phi^-}=-1.
```

Their difference is stored entirely in joint correlation structure.

---

## 19. Common misconceptions

### Misconception 1: "Correlation means entanglement."

False. Classically correlated separable states exist.

### Misconception 2: "Every entangled state violates every Bell inequality."

False. Bell nonlocality is a stronger operational property in a specified measurement scenario.

### Misconception 3: "More entanglement always means a better quantum algorithm."

False. Utility is task-dependent, and excessive entanglement may make training or control harder.

### Misconception 4: "A maximally mixed local state means the global state is noisy."

False. A subsystem of a pure maximally entangled state can be maximally mixed.

### Misconception 5: "Entanglement proves quantum advantage."

False. Advantage requires a task-level comparison and resource analysis.

---

## 20. Connections to later chapters

This chapter feeds directly into:

- [Density Matrices and Mixed States](07-density-matrices.md),
- [Measurements and POVMs](08-measurements-and-povms.md),
- [Entanglement Theory](../06-quantum-information-theory/03-entanglement-theory.md),
- [Quantum Resource Theories](../06-quantum-information-theory/04-resource-theories.md),
- [Quantum Communication](../06-quantum-information-theory/05-quantum-communication.md),
- [QCNNs and Structured Architectures](../07-quantum-machine-learning/05-qcnn.md),
- and the analysis of quantum advantage in learning.

---

## 21. Exercises

### A. Conceptual

1. Explain why a pure entangled state can have mixed local reduced states.
2. What does Schmidt rank measure?
3. Why are the Schmidt coefficients the same for both reduced states of a bipartite pure state?
4. Give the conceptual difference between entanglement and Bell nonlocality.
5. Why is entanglement not sufficient to prove computational advantage?

### B. Computational

6. Determine whether

```math
|\psi\rangle
=
\frac{|00\rangle+2|01\rangle+|10\rangle+2|11\rangle}{\sqrt{10}}
```

is entangled.

7. For

```math
|\psi(p)\rangle
=
\sqrt p|00\rangle
+
\sqrt{1-p}|11\rangle,
```

compute $\rho_A$ and its purity.

8. Show that the entanglement entropy of a Bell state is one bit.
9. Compute $\langle Z\otimes Z\rangle$ for both $|\Phi^+\rangle$ and $\rho_{\mathrm{cc}}$.
10. Compute $\langle X\otimes X\rangle$ for the same two states and explain why this distinguishes coherent entanglement from the classical mixture.

### C. Research-oriented

11. Find an example of an efficiently classically simulable circuit family that can nevertheless generate entanglement. Explain why this defeats the slogan "entanglement implies quantum hardness."
12. In a variational model, what experiment would separate the effect of entanglement from the effect of simply increasing parameter count?
13. Suppose a QML model only measures single-qubit observables. What entanglement-dependent information could remain hidden?
14. Propose a resource-aware question that is stronger than "does the model generate entanglement?"

---

## 22. Key takeaways

- Pure-state entanglement is failure of tensor-product factorization.
- Schmidt decomposition is the canonical representation of bipartite pure-state entanglement.
- Schmidt coefficients determine the reduced-state spectra and entanglement entropy.
- Classical correlation and entanglement are different resources.
- Mixed-state separability is a convex-decomposition condition.
- Bell nonlocality and entanglement are related but not identical.
- Entanglement is useful only relative to a task and allowed operations.
- Entanglement alone does not prove classical hardness, trainability, or quantum advantage.

---

## References

1. R. Horodecki, P. Horodecki, M. Horodecki, and K. Horodecki, "Quantum entanglement," *Reviews of Modern Physics* 81, 865 (2009). https://doi.org/10.1103/RevModPhys.81.865
2. J. S. Bell, "On the Einstein Podolsky Rosen paradox," *Physics Physique Fizika* 1, 195 (1964). https://doi.org/10.1103/PhysicsPhysiqueFizika.1.195
3. J. F. Clauser, M. A. Horne, A. Shimony, and R. A. Holt, "Proposed experiment to test local hidden-variable theories," *Physical Review Letters* 23, 880 (1969). https://doi.org/10.1103/PhysRevLett.23.880
4. C. H. Bennett et al., "Teleporting an unknown quantum state via dual classical and EPR channels," *Physical Review Letters* 70, 1895 (1993). https://doi.org/10.1103/PhysRevLett.70.1895
5. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
