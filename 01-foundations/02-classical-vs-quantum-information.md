# Classical vs Quantum Information

## 1. Why this distinction matters

Quantum information is not obtained by taking ordinary classical probabilities and making them more complicated. The decisive change is that quantum theory assigns **complex amplitudes** to alternatives, while observable probabilities arise only after a measurement rule is applied.

This introduces structure that classical probability does not contain: relative phase, interference, incompatible measurements, and state disturbance. These ideas are the conceptual basis of quantum algorithms and later become central when asking what a quantum machine-learning model can do that a classical model cannot.

### Learning objectives

After this chapter, you should be able to:

- distinguish a classical bit, a classical random bit, and a qubit,
- explain the difference between probabilities and probability amplitudes,
- distinguish global phase from relative phase,
- derive the simplest interference experiment using the Hadamard gate,
- distinguish a coherent superposition from a classical statistical mixture,
- explain why measurement basis matters,
- derive the no-cloning obstruction from linearity,
- and state why an exponentially large Hilbert space is not by itself a proof of computational advantage.

### Prerequisites

Only elementary complex numbers, vectors, and probability are assumed. Density matrices appear briefly as a preview and are developed systematically in [Density Matrices and Mixed States](07-density-matrices.md).

---

## 2. Classical information

### 2.1 A deterministic bit

A classical bit has one of two values:

```math
b\in\{0,1\}.
```

A register of $n$ bits stores one string

```math
x=x_1x_2\cdots x_n\in\{0,1\}^n.
```

There are $2^n$ possible strings, but at any instant an ideal deterministic classical register contains one of them.

### 2.2 A random bit

If we are uncertain about the bit value, we describe it using probabilities

```math
p_0=P(b=0),
\qquad
p_1=P(b=1),
```

with

```math
p_0\ge0,
\qquad
p_1\ge0,
\qquad
p_0+p_1=1.
```

For a fair random bit,

```math
p_0=p_1=\frac12.
```

The probability vector is therefore

```math
p=
\begin{pmatrix}
1/2\\
1/2
\end{pmatrix}.
```

Classical randomness represents uncertainty about which alternative occurs. The probabilities themselves do not carry a phase that can later produce constructive or destructive interference.

### 2.3 Reversible and stochastic classical dynamics

A reversible classical transformation permutes basis states. For one bit, the nontrivial reversible transformation is NOT:

```math
0\mapsto1,
\qquad
1\mapsto0.
```

More general noisy classical dynamics are stochastic maps. If $p$ is a probability vector, then

```math
p' = T p,
```

where $T$ has nonnegative entries and preserves normalization.

This is the classical reference point against which quantum states and quantum dynamics should be compared.

---

## 3. Quantum amplitudes

A pure qubit state is written

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle,
```

where

```math
\alpha,\beta\in\mathbb C
```

and normalization requires

```math
|\alpha|^2+|\beta|^2=1.
```

The coefficients $\alpha$ and $\beta$ are **probability amplitudes**, not probabilities.

If the qubit is measured in the computational basis, the Born rule gives

```math
P(0)=|\alpha|^2,
\qquad
P(1)=|\beta|^2.
```

The squaring of magnitudes is crucial. Two states may produce the same probabilities in one basis while remaining physically distinguishable because their relative phases differ.

---

## 4. Phase: what is physical and what is not?

### 4.1 Global phase

Consider

```math
|\psi'\rangle=e^{i\gamma}|\psi\rangle.
```

For any projector $P$, the probability of the corresponding outcome is

```math
\langle\psi'|P|\psi'\rangle
=
e^{-i\gamma}e^{i\gamma}
\langle\psi|P|\psi\rangle
=
\langle\psi|P|\psi\rangle.
```

Therefore a common phase multiplying the whole state is physically irrelevant:

```math
|\psi\rangle
\sim
e^{i\gamma}|\psi\rangle.
```

Pure physical states are therefore represented by rays in Hilbert space rather than by individual normalized vectors.

### 4.2 Relative phase

Now compare

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}
```

and

```math
|-\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt2}.
```

Both give

```math
P(0)=P(1)=\frac12
```

when measured in the computational basis.

However,

```math
\langle+|-\rangle=0,
```

so they are orthogonal and perfectly distinguishable in a suitable basis. The sign between the amplitudes is a **relative phase**, and relative phase is physically meaningful.

---

## 5. Interference from first principles

The Hadamard gate is

```math
H=
\frac1{\sqrt2}
\begin{pmatrix}
1&1\\
1&-1
\end{pmatrix}.
```

Its action on the computational basis is

```math
H|0\rangle=|+\rangle,
\qquad
H|1\rangle=|-\rangle.
```

Applying $H$ again gives

```math
H|+\rangle=|0\rangle,
\qquad
H|-\rangle=|1\rangle.
```

Let us derive the first identity explicitly:

```math
H|+\rangle
=
H\frac{|0\rangle+|1\rangle}{\sqrt2}
=
\frac{H|0\rangle+H|1\rangle}{\sqrt2}.
```

Substituting the two Hadamard outputs,

```math
H|+\rangle
=
\frac1{2}
\left[
(|0\rangle+|1\rangle)
+
(|0\rangle-|1\rangle)
\right].
```

The $|1\rangle$ amplitudes cancel:

```math
H|+\rangle=|0\rangle.
```

For $|-\rangle$, the opposite cancellation occurs and the $|0\rangle$ component disappears.

This is the basic mechanism of quantum interference:

```text
amplitudes combine first
→ phases affect the combination
→ probabilities are computed afterwards
```

A quantum algorithm is useful only if it arranges these amplitudes so that useful information becomes likely to appear in measurement outcomes.

---

## 6. A general phase experiment

Consider the family

```math
|\psi_\phi\rangle
=
\frac{|0\rangle+e^{i\phi}|1\rangle}{\sqrt2}.
```

Computational-basis probabilities are independent of $\phi$:

```math
P(0)=P(1)=\frac12.
```

Now apply a Hadamard gate:

```math
H|\psi_\phi\rangle
=
\frac12
\left[
(1+e^{i\phi})|0\rangle
+
(1-e^{i\phi})|1\rangle
\right].
```

The output probabilities are

```math
P_H(0)
=
\frac14|1+e^{i\phi}|^2
=
\frac{1+\cos\phi}{2},
```

and

```math
P_H(1)
=
\frac14|1-e^{i\phi}|^2
=
\frac{1-\cos\phi}{2}.
```

Equivalently,

```math
P_H(0)=\cos^2\frac\phi2,
\qquad
P_H(1)=\sin^2\frac\phi2.
```

The phase that was invisible in one measurement basis becomes directly observable after a change of basis.

This is a recurring pattern in quantum computing: information may be stored in phase and then converted into measurable population differences by interference.

---

## 7. Superposition is not classical uncertainty

A common misconception is that

```math
\frac{|0\rangle+|1\rangle}{\sqrt2}
```

means "the system is really either $0$ or $1$, but we do not know which one."

That interpretation predicts the wrong physics.

For the coherent state $|+\rangle$, the density matrix is

```math
\rho_+
=
|+\rangle\langle+|
=
\frac12
\begin{pmatrix}
1&1\\
1&1
\end{pmatrix}.
```

A classical 50/50 mixture of $|0\rangle$ and $|1\rangle$ has density matrix

```math
\rho_{\mathrm{mix}}
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|
=
\frac12
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix}.
```

Both give the same computational-basis probabilities, but they behave differently under a Hadamard gate.

For the coherent state,

```math
H\rho_+H^\dagger
=|0\rangle\langle0|.
```

For the mixture,

```math
H\rho_{\mathrm{mix}}H^\dagger
=\frac I2
=\rho_{\mathrm{mix}}.
```

The off-diagonal matrix elements encode coherence between the basis alternatives. They are exactly what the classical mixture lacks.

---

## 8. Measurement basis matters

A quantum state does not come with a single classical probability distribution that answers every possible question about it.

For $|0\rangle$:

- measurement in the $Z$ basis gives $0$ with certainty,
- measurement in the $X$ basis gives $+$ and $-$ with equal probability.

The same state therefore induces different probability distributions under different measurements.

This is why the pair

```math
(\rho,\text{measurement})
```

is operationally fundamental. A state alone does not specify the classical data that will be observed.

The general formalism of projective measurements and POVMs is developed in [Measurements and POVMs](08-measurements-and-povms.md).

---

## 9. Unknown quantum states cannot be cloned perfectly

Suppose there were a unitary $U$ that copied every pure state using a blank state $|0\rangle$:

```math
U|\psi\rangle|0\rangle
=
|\psi\rangle|\psi\rangle.
```

For two arbitrary states $|\psi\rangle$ and $|\phi\rangle$, unitarity preserves inner products. Therefore

```math
\langle\psi|\phi\rangle
=
\langle\psi|\phi\rangle^2.
```

Let

```math
c=\langle\psi|\phi\rangle.
```

Then the cloning assumption requires

```math
c=c^2.
```

The only solutions are

```math
c=0
\quad\text{or}\quad
c=1.
```

Thus a single device may perfectly clone mutually orthogonal states or identical states, but it cannot perfectly clone an arbitrary unknown pair of nonorthogonal states.

The no-cloning theorem is not an engineering limitation. It follows from the linear structure of quantum mechanics.

---

## 10. Many classical bits versus many qubits

An $n$-qubit pure state has the form

```math
|\psi\rangle
=
\sum_{x\in\{0,1\}^n}
\alpha_x|x\rangle,
```

with

```math
\sum_x|\alpha_x|^2=1.
```

There are $2^n$ complex amplitudes in a computational-basis description. This exponential dimension is mathematically important, but it must be interpreted carefully.

A measurement of the register does **not** reveal all $2^n$ amplitudes. A computational-basis measurement returns one bit string $x$ sampled with probability

```math
P(x)=|\alpha_x|^2.
```

Therefore the statement

> "an $n$-qubit register stores $2^n$ classical numbers that can all be read out"

is incorrect.

The challenge of quantum algorithm design is to transform global amplitude information into a small number of useful measurement statistics.

---

## 11. Worked example: phase without population change

Consider

```math
|\psi\rangle
=
\frac{|0\rangle+i|1\rangle}{\sqrt2}.
```

### Step 1: normalization

```math
\left|\frac1{\sqrt2}\right|^2
+
\left|\frac i{\sqrt2}\right|^2
=
\frac12+\frac12=1.
```

The state is normalized.

### Step 2: computational-basis measurement

```math
P(0)=P(1)=\frac12.
```

These probabilities are identical to those of $|+\rangle$ and $|-\rangle$.

### Step 3: identify the relative phase

The relative phase is

```math
\phi=\frac\pi2.
```

### Step 4: apply Hadamard and measure

Using the general result above,

```math
P_H(0)
=
\frac{1+\cos(\pi/2)}2
=
\frac12,
```

and

```math
P_H(1)=\frac12.
```

A Hadamard measurement alone does not distinguish this state deterministically from all other equatorial states. To access the full phase one needs complementary measurements, which motivates the Bloch-sphere description.

---

## 12. Worked example: pure superposition versus mixture

Compare

```math
\rho_1=|+\rangle\langle+|
```

with

```math
\rho_2=\frac I2.
```

In the $Z$ basis, both produce a fair bit.

Now measure $X$.

Because $|+\rangle$ is the $+1$ eigenstate of $X$,

```math
P_{\rho_1}(X=+1)=1.
```

For the maximally mixed state,

```math
P_{\rho_2}(X=+1)=\frac12.
```

The states are therefore operationally distinguishable even though one particular measurement produces identical statistics.

---

## 13. Where quantum computational advantage can come from

The existence of superposition or an exponentially large Hilbert space does not automatically imply speedup.

A rigorous advantage claim must specify at least:

1. the computational or learning task,
2. the input-access model,
3. the quantum resource being used,
4. the cost measure,
5. and the classical competitor.

Quantum algorithms may exploit resources such as

- coherent phase processing,
- interference,
- entanglement,
- noncommuting observables,
- coherent oracle access,
- quantum memory,
- or direct access to quantum data.

But the relevant question is always operational:

> What useful quantity can be obtained with fewer resources than under the best relevant classical model?

This discipline will become especially important in the quantum-machine-learning chapters.

---

## 14. Common misconceptions

### Misconception 1: "A qubit is simultaneously a classical 0 and a classical 1."

A qubit is a vector in a complex two-dimensional Hilbert space. The statement above hides the essential role of amplitudes and relative phase.

### Misconception 2: "A superposition is just classical uncertainty."

False. Coherent superpositions contain off-diagonal terms and can interfere. Classical mixtures do not.

### Misconception 3: "Quantum parallelism evaluates every answer and lets us read them all."

False. Measurement returns restricted classical information. The algorithm must engineer interference so the desired information is concentrated into accessible observables.

### Misconception 4: "Any phase is physically observable."

Only relative phase matters. A global phase has no effect on measurement probabilities.

### Misconception 5: "Measurement merely reveals a pre-existing classical value."

That intuition is generally inadequate. Measurement statistics depend on the chosen observable, and incompatible observables cannot all be treated as one ordinary joint classical random variable.

---

## 15. Connections to later chapters

This chapter connects directly to:

- [Qubits and Hilbert Spaces](03-qubits-and-hilbert-spaces.md): formal vector-space language,
- [The Bloch Sphere](04-bloch-sphere.md): geometric representation of relative phase and measurement directions,
- [Density Matrices and Mixed States](07-density-matrices.md): precise distinction between coherence and classical mixtures,
- [Measurements and POVMs](08-measurements-and-povms.md): the state-measurement interface,
- [Gate-Based Quantum Computing](../02-quantum-computing/01-gate-model.md): interference as a computational primitive,
- [What Is QML?](../07-quantum-machine-learning/01-what-is-qml.md): identifying genuinely quantum learning resources.

---

## 16. Exercises

### A. Conceptual

1. Why can two states have identical computational-basis probabilities and still be physically different?
2. Explain the difference between a global phase and a relative phase.
3. Why is a coherent superposition not equivalent to ignorance about a hidden classical state?
4. Why does the dimension $2^n$ of the $n$-qubit Hilbert space not automatically imply an exponential algorithmic speedup?
5. Explain why measurement should be treated as part of an information-processing protocol rather than as a passive final step.

### B. Computational

6. Verify that

```math
|\psi\rangle
=
\frac{\sqrt3}{2}|0\rangle
+
\frac{i}{2}|1\rangle
```

is normalized, and compute computational-basis probabilities.

7. For

```math
|\psi_\phi\rangle
=
\frac{|0\rangle+e^{i\phi}|1\rangle}{\sqrt2},
```

derive $P_H(0)$ and $P_H(1)$ after a Hadamard gate without using the result from the text.

8. Show directly that

```math
|+\rangle\langle+|
\neq
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|.
```

9. Suppose two normalized states satisfy

```math
\langle\psi|\phi\rangle=\frac12.
```

Use the no-cloning argument to show why a perfect universal cloner cannot clone both states.

10. Compute the result of

```math
H
\left(
\frac{|0\rangle-|1\rangle}{\sqrt2}
\right).
```

Explain the result using interference rather than matrix multiplication alone.

### C. Research-oriented

11. Give an example of a quantum algorithm where phase information is converted into a measurable quantity by interference. Identify exactly where the conversion occurs.
12. Formulate a precise statement explaining why "exponentially large feature space" is insufficient by itself to establish quantum advantage in machine learning.
13. Compare two possible resource claims: "uses entanglement" and "achieves lower query complexity." Which is operationally stronger, and why?
14. Suppose a learning model only ever measures in one fixed basis. What quantum information might remain inaccessible to it?

---

## 17. Key takeaways

- Classical probabilities and quantum amplitudes are different mathematical objects.
- Probabilities depend on amplitude magnitudes, while relative phases control interference.
- Global phase is physically irrelevant; relative phase is observable through suitable transformations and measurements.
- A coherent superposition is not equivalent to a classical mixture.
- Measurement basis determines which information becomes classical data.
- No-cloning follows from the linear structure of quantum mechanics.
- Exponential Hilbert-space dimension is a resource opportunity, not a proof of quantum advantage.

---

## References

1. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
2. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
3. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
4. W. K. Wootters and W. H. Zurek, "A single quantum cannot be cloned," *Nature* 299, 802–803 (1982). https://doi.org/10.1038/299802a0
5. D. Dieks, "Communication by EPR devices," *Physics Letters A* 92, 271–272 (1982). https://doi.org/10.1016/0375-9601(82)90084-6
