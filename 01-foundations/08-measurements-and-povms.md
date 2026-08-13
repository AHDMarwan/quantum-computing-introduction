# Measurements and POVMs

## 1. Measurement is the quantum-to-classical interface

A quantum state is not directly readable as a table of amplitudes. A measurement is a physical operation that converts quantum information into a classical outcome according to probabilities determined jointly by the state and the chosen measurement.

This has a major consequence: the object that produces observable data is not the state alone, but the pair

```math
(\rho,\text{measurement}).
```

The same state can produce completely different classical probability distributions under different measurements.

This is central to quantum algorithms, communication, sensing, tomography, and quantum machine learning.

### Learning objectives

After this chapter, you should be able to:

- derive projective-measurement probabilities from the Born rule,
- distinguish observables, projectors, POVM elements, and measurement instruments,
- compute expectation values and variances,
- describe post-measurement states,
- understand noncommuting observables and measurement incompatibility,
- estimate the sampling cost of expectation values,
- formulate state discrimination as POVM optimization,
- and explain why measurement design can itself be part of a quantum learning problem.

---

## 2. Projective measurements

Let a Hermitian observable have spectral decomposition

```math
A
=
\sum_a aP_a,
```

where $P_a$ are orthogonal projectors satisfying

```math
P_aP_b
=
\delta_{ab}P_a,
```

and

```math
\sum_aP_a=I.
```

If the system is in state $\rho$, the Born rule gives

```math
p(a)
=
\mathrm{Tr}(P_a\rho).
```

For a pure state

```math
\rho=|\psi\rangle\langle\psi|,
```

this becomes

```math
p(a)
=
\langle\psi|P_a|\psi\rangle.
```

If the eigenspace is one-dimensional,

```math
P_a=|a\rangle\langle a|,
```

then

```math
p(a)
=
|\langle a|\psi\rangle|^2.
```

---

## 3. Computational-basis measurement

For one qubit,

```math
P_0=|0\rangle\langle0|,
```

and

```math
P_1=|1\rangle\langle1|.
```

If

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle,
```

then

```math
p(0)=|\alpha|^2,
```

```math
p(1)=|\beta|^2.
```

For an $n$-qubit state

```math
|\psi\rangle
=
\sum_{z\in\{0,1\}^n}
\alpha_z|z\rangle,
```

computational-basis measurement returns one bit string $z$ with probability

```math
p(z)=|\alpha_z|^2.
```

A single shot does not reveal the full probability distribution. Repeated preparation and measurement are needed to estimate it.

---

## 4. Expectation values

For an observable

```math
A=\sum_a aP_a,
```

the expectation value is

```math
\mathbb E[A]
=
\sum_a a\,p(a).
```

Using the Born rule,

```math
\mathbb E[A]
=
\sum_a a\,\mathrm{Tr}(P_a\rho).
```

By linearity of the trace,

```math
\mathbb E[A]
=
\mathrm{Tr}(A\rho).
```

Thus

```math
\langle A\rangle_\rho
=
\mathrm{Tr}(\rho A).
```

For a pure state,

```math
\langle A\rangle
=
\langle\psi|A|\psi\rangle.
```

This trace rule is the basic readout formula in variational quantum algorithms and many QML models.

---

## 5. Variance and statistical uncertainty

The variance of observable $A$ is

```math
\mathrm{Var}(A)
=
\langle A^2\rangle
-
\langle A\rangle^2.
```

If an expectation value is estimated from $N$ independent measurement shots, the standard error of the sample mean scales as

```math
\frac{\sqrt{\mathrm{Var}(A)}}{\sqrt N}.
```

For bounded observables, this gives the generic Monte Carlo scaling

```math
O(N^{-1/2}).
```

Therefore reducing statistical error by a factor of ten generally requires roughly one hundred times more independent shots.

Measurement cost is therefore part of quantum-algorithm complexity.

---

## 6. Post-measurement states for projective measurements

Outcome probabilities do not fully describe measurement. A measurement can also transform the quantum state.

For an ideal projective measurement with outcome $a$, the conditional post-measurement state is

```math
\rho_a
=
\frac{P_a\rho P_a}
{\mathrm{Tr}(P_a\rho)}.
```

For a pure state,

```math
|\psi_a\rangle
=
\frac{P_a|\psi\rangle}
{\sqrt{\langle\psi|P_a|\psi\rangle}}.
```

If the outcome is ignored, the nonselective post-measurement state is

```math
\rho'
=
\sum_aP_a\rho P_a.
```

This can remove coherence between different measurement eigenspaces.

---

## 7. Worked example: measuring $Z$ on $|+\rangle$

Start from

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}.
```

The two outcome probabilities are

```math
p(0)=p(1)=\frac12.
```

If outcome $0$ occurs, the post-measurement state is

```math
|0\rangle.
```

If outcome $1$ occurs, the post-measurement state is

```math
|1\rangle.
```

If we perform the measurement but discard the outcome, the final density operator is

```math
\rho'
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|
=
\frac I2.
```

The original phase coherence has been destroyed by the measurement interaction.

---

## 8. Measuring in another basis

To measure $X$, use the eigenstates

```math
|+\rangle,
\qquad
|-\rangle.
```

The projectors are

```math
P_+
=|+\rangle\langle+|,
```

```math
P_-
=|-\rangle\langle-|.
```

Operationally, an $X$ measurement can be implemented by applying a Hadamard gate and then measuring in the computational basis:

```text
X-basis measurement
=
H
→ Z-basis measurement
```

This is an example of **basis rotation before readout**.

Similar basis changes are used constantly when estimating Pauli observables on quantum hardware.

---

## 9. General measurements: POVMs

Projective measurements are not the most general measurements allowed by quantum theory.

A positive-operator-valued measure (POVM) is a set of positive semidefinite operators

```math
\{E_y\}_y
```

satisfying

```math
E_y\succeq0
```

and

```math
\sum_yE_y=I.
```

The probability of outcome $y$ is

```math
p(y)
=
\mathrm{Tr}(E_y\rho).
```

Unlike projective measurement operators, POVM elements need not satisfy

```math
E_yE_{y'}=\delta_{yy'}E_y.
```

They need not be mutually orthogonal projectors.

This additional freedom is important in state discrimination and optimal information extraction.

---

## 10. A simple nonprojective POVM

Consider three pure qubit states whose Bloch vectors lie $120^\circ$ apart in the equatorial plane. Let the corresponding state projectors be

```math
|\psi_1\rangle\langle\psi_1|,
\quad
|\psi_2\rangle\langle\psi_2|,
\quad
|\psi_3\rangle\langle\psi_3|.
```

A symmetric three-outcome POVM can be constructed as

```math
E_j
=
\frac23
|\psi_j\rangle\langle\psi_j|.
```

These operators are positive and satisfy

```math
\sum_{j=1}^3E_j=I.
```

A two-dimensional Hilbert space therefore supports a measurement with three classical outcomes.

This cannot be represented as an ordinary nondegenerate projective measurement on the same qubit alone.

---

## 11. POVM probabilities do not determine the state update

A POVM specifies outcome probabilities, but not the complete physical transformation after the measurement.

Suppose measurement operators $M_y$ satisfy

```math
E_y=M_y^\dagger M_y.
```

Then

```math
p(y)
=
\mathrm{Tr}(M_y\rho M_y^\dagger)
=
\mathrm{Tr}(E_y\rho).
```

The conditional post-measurement state is

```math
\rho_y
=
\frac{M_y\rho M_y^\dagger}{p(y)}.
```

Different sets of $M_y$ can generate the same POVM elements $E_y$ while producing different post-measurement states.

Thus:

```text
POVM      → outcome statistics
instrument → outcome statistics + state update
```

---

## 12. Quantum instruments

A quantum instrument associates each outcome $y$ with a completely positive map $\mathcal I_y$.

The outcome probability is

```math
p(y)
=
\mathrm{Tr}[\mathcal I_y(\rho)].
```

The normalized conditional state is

```math
\rho_y
=
\frac{\mathcal I_y(\rho)}{p(y)}.
```

If outcomes are ignored, the overall channel is

```math
\mathcal E
=
\sum_y\mathcal I_y.
```

Instruments are essential for:

- adaptive measurements,
- sequential decision protocols,
- feedback control,
- quantum trajectories,
- and learning problems in which future actions depend on previous measurement outcomes.

---

## 13. Naimark-dilation viewpoint

A general POVM can be understood as a projective measurement on a larger Hilbert space after coupling the system to an ancilla.

Conceptually:

```text
system
+ ancilla
→ joint unitary
→ projective measurement
→ effective POVM on system
```

This is useful because it shows that generalized measurements do not require abandoning ordinary unitary quantum mechanics. They can emerge from ordinary dynamics on a larger system followed by projective readout.

---

## 14. Noncommuting observables

Two observables $A$ and $B$ commute if

```math
[A,B]
=
AB-BA
=0.
```

If

```math
[A,B]\neq0,
```

they generally do not admit a common complete eigenbasis.

For Pauli matrices,

```math
[X,Z]
=-2iY
\neq0.
```

An eigenstate of $Z$ is therefore not generally an eigenstate of $X$.

This is the mathematical basis of measurement incompatibility.

---

## 15. Uncertainty relation

For observables $A$ and $B$, define

```math
(\Delta A)^2
=
\langle A^2\rangle
-
\langle A\rangle^2.
```

The Robertson uncertainty relation is

```math
\Delta A\,\Delta B
\ge
\frac12
\left|
\langle[A,B]\rangle
\right|.
```

For $X$ and $Z$,

```math
[X,Z]=-2iY.
```

Thus states with sharply defined $Z$ need not have sharply defined $X$.

The uncertainty relation is not merely a statement about defective measurement devices. It reflects incompatibility in the operator structure of quantum theory.

---

## 16. Measurement disturbance versus uncertainty

Two ideas are often mixed together:

1. **preparation uncertainty**: a state cannot generally have zero variance for two incompatible observables,
2. **measurement disturbance**: performing one measurement can change statistics of a later measurement.

They are related but not identical.

The Robertson relation concerns statistical spreads in a state. It is not, by itself, a universal quantitative statement about how much one measurement physically disturbs another.

---

## 17. State discrimination as a measurement-design problem

Suppose a source prepares state $\rho_x$ with prior probability $p_x$. A learner receives the unknown state and must guess $x$.

Choose a POVM

```math
\{E_x\}_x.
```

The success probability is

```math
P_{\mathrm{succ}}
=
\sum_x
p_x
\mathrm{Tr}(E_x\rho_x).
```

The optimal discrimination problem is

```math
\max_{\{E_x\}}
\sum_x
p_x
\mathrm{Tr}(E_x\rho_x)
```

subject to

```math
E_x\succeq0,
```

and

```math
\sum_xE_x=I.
```

Thus the measurement itself is an optimization variable.

This is an important conceptual bridge toward quantum machine learning: sometimes the learning model should be viewed not as a trainable unitary followed by a fixed measurement, but as a trainable measurement strategy.

---

## 18. Binary Helstrom discrimination

For two states $\rho_0$ and $\rho_1$ with equal prior probabilities, the optimal success probability is

```math
P_{\mathrm{succ}}^*
=
\frac12
\left[
1+D(\rho_0,\rho_1)
\right],
```

where

```math
D(\rho_0,\rho_1)
=
\frac12
\|\rho_0-\rho_1\|_1.
```

If the states are identical,

```math
D=0,
```

so

```math
P_{\mathrm{succ}}^*=\frac12.
```

No measurement can outperform random guessing.

If the states are orthogonal,

```math
D=1,
```

so

```math
P_{\mathrm{succ}}^*=1.
```

They can be distinguished perfectly.

---

## 19. Worked example: discriminate $|0\rangle$ and $|+\rangle$

Consider equal priors for

```math
|\psi_0\rangle=|0\rangle,
```

and

```math
|\psi_1\rangle=|+\rangle.
```

Their overlap is

```math
|\langle0|+\rangle|^2
=
\frac12.
```

For two pure states with equal priors, the optimal success probability can be written

```math
P_{\mathrm{succ}}^*
=
\frac12
\left(
1+
\sqrt{1-|\langle\psi_0|\psi_1\rangle|^2}
\right).
```

Therefore

```math
P_{\mathrm{succ}}^*
=
\frac12
\left(
1+\frac1{\sqrt2}
\right).
```

The states are nonorthogonal, so perfect one-copy discrimination is impossible.

---

## 20. Measurement shots and finite-sample estimation

Suppose $A$ has outcomes $\pm1$ and expectation value

```math
\mu=\langle A\rangle.
```

From $N$ independent shots, define

```math
\hat\mu
=
\frac1N
\sum_{j=1}^N a_j.
```

Then

```math
\mathbb E[\hat\mu]=\mu.
```

Its variance is

```math
\mathrm{Var}(\hat\mu)
=
\frac{1-\mu^2}{N}
\le
\frac1N.
```

Therefore the root-mean-square statistical error scales no worse than

```math
N^{-1/2}.
```

This matters enormously for VQE, QAOA, variational QML, and quantum kernels because training may require many expectation-value estimates.

---

## 21. Measurement grouping

Suppose a Hamiltonian or loss observable is decomposed as

```math
H
=
\sum_jc_jP_j,
```

where $P_j$ are Pauli strings.

Then

```math
\langle H\rangle
=
\sum_jc_j\langle P_j\rangle.
```

Naively, each $P_j$ may require a separate measurement setting. However, commuting terms can sometimes be measured together after an appropriate basis rotation.

Measurement grouping is therefore a resource-optimization problem: it changes the number of circuit executions required to estimate the same observable.

---

## 22. Tomography as repeated measurement design

To reconstruct an unknown state, one performs an informationally complete collection of measurements on many copies of the state.

For one qubit, estimating

```math
\langle X\rangle,
\qquad
\langle Y\rangle,
\qquad
\langle Z\rangle
```

is sufficient to reconstruct

```math
\rho
=
\frac12
\left[
I
+\langle X\rangle X
+\langle Y\rangle Y
+\langle Z\rangle Z
\right].
```

For large systems, full tomography becomes expensive because the number of parameters grows rapidly with Hilbert-space dimension.

This motivates compressed, task-specific, shadow-based, or directly quantum learning strategies that avoid reconstructing the entire state.

---

## 23. Measurement in quantum machine learning

Many variational QML models are written as

```math
f_\theta(x)
=
\mathrm{Tr}
\left[
M\rho_\theta(x)
\right],
```

where

- $\rho_\theta(x)$ is the encoded and processed quantum state,
- $M$ is a measurement observable,
- and the expectation value becomes a model output.

A common implicit assumption is that $M$ is fixed while the circuit is trainable.

But quantum decision theory suggests a broader possibility:

```text
fixed or structured state preparation
+
trainable POVM / adaptive instrument
```

The measurement strategy can itself be the hypothesis class.

This is especially natural for learning directly from quantum data.

---

## 24. Common misconceptions

### Misconception 1: "Measurement reads the wavefunction."

False. A single measurement returns a classical outcome, not the full state description.

### Misconception 2: "POVM means a noisy projective measurement."

Not necessarily. POVMs are the general mathematical description of outcome statistics and can be optimal even in ideal protocols.

### Misconception 3: "The POVM determines the post-measurement state."

No. The POVM determines probabilities. A quantum instrument specifies the state update.

### Misconception 4: "Noncommuting observables are impossible to measure."

Each can be measured individually. The issue is that they cannot generally be treated as simultaneously sharp compatible observables on the same state preparation.

### Misconception 5: "Expectation values are exact outputs of quantum hardware."

Typically they are estimated statistically from finite samples.

### Misconception 6: "Measurement is only the last step of a quantum algorithm."

Not always. Measurements can occur mid-circuit, adaptively, or as the main optimized object in a protocol.

---

## 25. Connections to later chapters

Measurement theory connects directly to:

- [Quantum Channels](../06-quantum-information-theory/01-quantum-channels.md),
- [Quantum Communication](../06-quantum-information-theory/05-quantum-communication.md),
- [Optimization and Gradients](../05-variational-quantum-algorithms/05-optimization-and-gradients.md),
- [Quantum Kernel Methods](../07-quantum-machine-learning/04-quantum-kernels.md),
- [Learning from Quantum Data](../07-quantum-machine-learning/10-learning-from-quantum-data.md),
- and resource accounting for QML trainability and advantage.

---

## 26. Exercises

### A. Conceptual

1. Why is a measurement basis part of the information-processing protocol?
2. What is the difference between an observable and a POVM?
3. What additional information does a quantum instrument specify beyond a POVM?
4. Why can nonorthogonal states not be perfectly discriminated from one copy?
5. Why does shot noise matter for variational algorithms?

### B. Computational

6. For

```math
|\psi\rangle
=
\frac{\sqrt3}{2}|0\rangle
+
\frac12|1\rangle,
```

compute the probabilities and expectation value of a $Z$ measurement.

7. Compute $\langle X\rangle$ for the same state.
8. Let

```math
\rho
=
\frac12
\begin{pmatrix}
1&1/2\\
1/2&1
\end{pmatrix}.
```

Compute $p(+)$ and $p(-)$ for an $X$ measurement.

9. Verify that

```math
E_0
=
\frac23|0\rangle\langle0|,
```

```math
E_1
=
\frac23|\psi_1\rangle\langle\psi_1|,
```

```math
E_2
=
\frac23|\psi_2\rangle\langle\psi_2|
```

form a POVM when the three Bloch vectors are separated by $120^\circ$ in the equatorial plane.

10. A $\pm1$ observable has true expectation $\mu=0.6$. What is the variance of the sample mean after $N$ shots?
11. Compute the optimal equal-prior discrimination success probability for two pure states with overlap magnitude $1/3$.

### C. Research-oriented

12. Design a QML model in which the circuit is fixed but the measurement POVM is trainable. What would the parameters represent?
13. Compare the resource cost of full tomography with direct estimation of one task-relevant observable.
14. When can measurement grouping substantially change the practical cost of a variational algorithm without changing its formal circuit ansatz?
15. Explain how adaptive measurement can turn a static classification problem into a sequential decision problem.
16. What would it mean for noncommuting measurements to act as an inductive bias in a quantum learning model?

---

## 27. Key takeaways

- Measurement converts quantum states into classical outcomes through the Born rule.
- Projective measurements are a special case of POVMs.
- POVMs specify outcome probabilities; instruments additionally specify state updates.
- Noncommuting observables encode measurement incompatibility.
- Expectation values on hardware are statistical estimates with finite-shot cost.
- State discrimination is an optimization problem over measurements.
- Measurement design can itself be a computational or learning resource.
- In QML, the readout should not automatically be treated as a passive fixed endpoint.

---

## References

1. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
2. C. W. Helstrom, *Quantum Detection and Estimation Theory*, Academic Press, 1976.
3. A. S. Holevo, *Probabilistic and Statistical Aspects of Quantum Theory*, North-Holland, 1982.
4. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
