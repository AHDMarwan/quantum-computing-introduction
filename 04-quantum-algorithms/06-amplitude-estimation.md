# Quantum Amplitude Estimation

## 1. Why amplitude estimation matters

Quantum amplitude estimation (QAE) turns the Grover rotation angle into a numerical estimate of an unknown probability or expectation value. It is the canonical example of a **quadratic improvement in precision scaling** relative to ordinary Monte Carlo sampling under coherent-access assumptions.

The high-level contrast is

```math
O(1/\epsilon^2)
```

samples for standard Monte Carlo estimation of an additive error $\epsilon$, versus

```math
O(1/\epsilon)
```

coherent quantum uses of the relevant state-preparation/reflection primitives in ideal amplitude-estimation settings.

The phrase “quadratic speedup” is meaningful only after specifying what must be loaded coherently and how expensive those primitives are.

## 2. Learning objectives

After this chapter, you should be able to:

- formulate an estimation problem as an unknown amplitude $a$,
- derive the two-dimensional good-bad decomposition,
- connect amplitude amplification to an eigenphase problem,
- explain how QPE estimates the Grover rotation angle,
- convert a phase estimate into an estimate of $a$,
- distinguish sample complexity from coherent query complexity,
- identify state-preparation and reflection costs,
- compare textbook QAE with shallower modern variants,
- and audit end-to-end claims of quantum Monte Carlo advantage.

## 3. Problem formulation

Suppose a unitary $A$ prepares

```math
A|0\rangle
=
\sqrt{1-a}\,|\psi_0\rangle|0\rangle
+
\sqrt a\,|\psi_1\rangle|1\rangle,
```

where

```math
a\in[0,1]
```

is unknown.

The last qubit marks whether an outcome is “good.” Measuring it directly produces a Bernoulli random variable with success probability $a$.

The task is to estimate $a$ to additive error approximately $\epsilon$.

## 4. Classical Monte Carlo baseline

If we repeatedly prepare the state and measure the final qubit, the empirical mean

```math
\hat a
=
\frac1N\sum_{j=1}^{N}X_j
```

estimates $a$, where

```math
X_j\in\{0,1\}.
```

Its variance is

```math
\mathrm{Var}(\hat a)
=
\frac{a(1-a)}{N}.
```

Therefore the root-mean-square statistical error scales as

```math
O(N^{-1/2}).
```

To reach additive error scale $\epsilon$, standard independent sampling requires

```math
N=O(1/\epsilon^2)
```

samples, up to confidence factors and problem-dependent constants.

This $1/\sqrt N$ law is the target that QAE improves in the coherent-query model.

## 5. Good-bad geometry

Write the prepared state as

```math
|\Psi\rangle
=
\cos\theta|B\rangle
+
\sin\theta|G\rangle,
```

with

```math
a=\sin^2\theta,
```

where $|G\rangle$ and $|B\rangle$ are normalized good and bad components.

Amplitude amplification constructs a Grover-like operator $Q$ that acts as a rotation by $2\theta$ in the two-dimensional span

```math
\mathrm{span}\{|G\rangle,|B\rangle\}.
```

Instead of applying enough rotations merely to amplify success probability, amplitude estimation asks:

> Can we estimate the rotation angle $\theta$ itself?

If yes, then

```math
a=\sin^2\theta
```

can be recovered numerically.

## 6. Grover operator and eigenphases

A standard construction uses two reflections, one about the prepared initial state and one that flips the phase of the good subspace.

Schematically,

```math
Q
=
-S_{\Psi}S_G,
```

where $S_G$ marks the good subspace and $S_{\Psi}$ is the reflection associated with $A|0\rangle$.

In the good-bad plane, $Q$ has eigenvalues

```math
e^{\pm 2i\theta}.
```

Therefore amplitude estimation becomes a phase-estimation problem for the Grover operator.

This creates the conceptual chain

```text
probability a
-> amplitude angle theta
-> Grover eigenphase
-> phase estimation
-> numerical estimate of a
```

## 7. Textbook amplitude estimation

The original QAE algorithm applies quantum phase estimation to powers of $Q$.

QPE estimates a phase proportional to

```math
\theta.
```

The final estimate is then obtained from

```math
\tilde a
=
\sin^2\tilde\theta.
```

If the total coherent query budget is of order $M$, ideal QAE achieves an estimation error scaling of order

```math
O(1/M)
```

rather than the classical Monte Carlo scaling

```math
O(1/\sqrt M).
```

Equivalently, to obtain error $\epsilon$,

```math
M=O(1/\epsilon)
```

coherent uses are sufficient in the standard oracle model.

## 8. Why the improvement is quadratic

Classical sampling extracts information from independent outcomes. The standard error shrinks as

```math
\frac1{\sqrt N}.
```

QAE instead preserves coherence across repeated applications of the Grover operator. The unknown probability is encoded as a phase accumulation, and phase estimation resolves that phase with precision scaling like inverse coherent evolution length.

So the quantum improvement is not “more samples at once.” It comes from converting an amplitude into a phase and estimating that phase coherently.

## 9. Worked example

Suppose

```math
a=\frac14.
```

Then

```math
\sin^2\theta=\frac14,
```

so in the principal range

```math
\theta=\frac{\pi}{6}.
```

The Grover operator has relevant eigenphases

```math
e^{\pm i\pi/3}.
```

If phase estimation recovers an angle close to $\pi/6$, the probability estimate becomes

```math
\tilde a
=
\sin^2\left(\frac{\pi}{6}\right)
=
\frac14.
```

This example shows why the same two-dimensional rotation geometry appears in both Grover search and amplitude estimation.

## 10. From expectations to amplitudes

Many numerical problems involve estimating an expectation

```math
\mu
=
\mathbb E[f(X)].
```

If a bounded function is rescaled so that

```math
0\le f(x)\le1,
```

one can design a coherent circuit whose ancilla success probability equals

```math
\mu.
```

For example, prepare

```math
\sum_x\sqrt{p_x}|x\rangle
```

and apply a controlled rotation satisfying schematically

```math
|x\rangle|0\rangle
\longmapsto
|x\rangle
\left(
\sqrt{1-f(x)}|0\rangle
+
\sqrt{f(x)}|1\rangle
\right).
```

The probability of measuring the ancilla in $|1\rangle$ is then

```math
\sum_xp_xf(x)
=
\mathbb E[f(X)].
```

QAE can estimate this amplitude.

This is the route from amplitude estimation to quantum Monte Carlo applications.

## 11. The state-preparation problem

The previous construction hides a major cost. To obtain a meaningful end-to-end improvement, the quantum computer must efficiently implement:

- coherent preparation of the distribution $p_x$,
- coherent evaluation or encoding of $f(x)$,
- the inverse $A^\dagger$,
- good-state reflections,
- and controlled or repeated applications of the Grover operator.

If the distribution is supplied as a large arbitrary classical table, coherent loading may erase the nominal quadratic advantage.

Therefore the correct complexity question is not simply

```math
O(1/\epsilon)
\quad\text{versus}\quad
O(1/\epsilon^2).
```

It is closer to

```math
C_{\mathrm{quantum}}
=
O\!\left(
\frac{C_A+C_{\mathrm{reflect}}}{\epsilon}
\right)
```

versus the cost of the strongest relevant classical estimator.

## 12. Coherent depth

Textbook QAE inherits the deep controlled-power structure of QPE. This can require long coherent circuits involving

```math
Q,
Q^2,
Q^4,
\ldots
```

or equivalent long sequences.

Thus the query advantage can coexist with a demanding circuit-depth requirement.

This distinction motivates alternative amplitude-estimation algorithms that avoid a full QFT or trade coherent depth for more repetitions and classical postprocessing.

## 13. Modern variants

Later QAE variants include iterative, maximum-likelihood, and other QFT-free approaches.

These methods differ in:

- maximum circuit depth,
- number of circuit executions,
- adaptivity,
- classical inference,
- robustness to noise,
- and constant factors.

A shallower method can be more attractive on limited hardware even if the asymptotic query statement is less elegant than textbook QAE.

Therefore “amplitude estimation” should be treated as a family of algorithms, not one fixed circuit.

## 14. Applications

Potential application domains include:

- Monte Carlo integration,
- risk estimation,
- option-pricing subroutines,
- reliability estimation,
- expectation values inside larger quantum algorithms,
- and probabilistic numerical routines.

However, every application must be examined for efficient coherent input preparation and output requirements.

## 15. Resource accounting

A useful decomposition is

```math
C_{\mathrm{total}}
=
C_{\mathrm{load}}
+
C_A
+
C_{A^\dagger}
+
C_{\mathrm{reflections}}
+
C_{\mathrm{phase/estimation}}
+
C_{\mathrm{classical\ post}}.
```

Relevant resources include:

| Resource | Question |
|---|---|
| State-preparation calls | How often is $A$ used? |
| Inverse calls | Can $A^\dagger$ be implemented efficiently? |
| Reflection cost | How hard is good-state marking? |
| Coherent depth | How long are repeated Grover powers? |
| Ancilla qubits | Does the chosen QAE variant require a phase register? |
| Error tolerance | What additive/relative error is required? |
| Classical preprocessing | How is the distribution encoded? |

## 16. When the quadratic advantage matters most

The precision improvement is potentially most valuable when:

- high accuracy is required,
- the coherent state-preparation oracle is naturally available,
- each classical sample is expensive,
- and the quantum circuit can implement repeated coherent queries efficiently.

If only low precision is needed, or coherent data loading is expensive, constant factors and hardware overhead may dominate the asymptotic benefit.

## 17. Common misconceptions

### “QAE gives a universal quadratic runtime speedup for every Monte Carlo problem.”

No. The proven improvement is in an oracle/coherent-query model. End-to-end speedup depends on data preparation and circuit cost.

### “QAE uses $O(1/\epsilon)$ ordinary independent samples.”

No. Its advantage relies on coherent applications of quantum operations, not ordinary classical samples.

### “QAE is just Grover search.”

They share the same rotation geometry, but the task differs: Grover amplifies success; QAE estimates the angle/probability.

### “The original QAE circuit is always the best practical version.”

No. Alternative variants can reduce coherent depth at the expense of other resources.

## 18. Connections

Amplitude estimation unifies several earlier ideas:

- Grover rotations,
- amplitude amplification,
- phase kickback,
- quantum phase estimation,
- Monte Carlo estimation,
- and coherent numerical algorithms.

It is also a useful template for understanding quantum advantage claims in QML: a better asymptotic subroutine does not imply an end-to-end advantage unless input access and output costs are included.

## 19. Exercises

### Conceptual

1. Why does ordinary Monte Carlo have $1/\sqrt N$ statistical-error scaling?
2. Why must QAE use coherent access rather than independent classical samples to achieve its improved scaling?
3. Explain the difference between amplitude amplification and amplitude estimation.
4. Why can state preparation eliminate an apparent query advantage?

### Computational

5. If $a=1/2$, compute the principal value of $\theta$ satisfying $a=\sin^2\theta$.
6. If an algorithm has classical sampling error proportional to $N^{-1/2}$, how many samples are needed to reduce error by a factor of 10?
7. Under ideal $1/M$ QAE scaling, how much must the coherent query budget increase to reduce error by a factor of 10?
8. Show that the controlled-rotation construction gives ancilla success probability $\sum_xp_xf(x)$.

### Research-oriented

9. A financial QAE proposal assumes a probability distribution can be loaded in polylogarithmic time. Why is this assumption potentially decisive?
10. Compare two QAE variants using total oracle calls, maximum coherent depth, ancilla count, and classical postprocessing.
11. Suppose a classical quasi-Monte Carlo method achieves better problem-specific scaling than naive Monte Carlo. How should the claimed quantum advantage be reevaluated?
12. Identify a setting where the data-generating process is already quantum, making coherent state preparation more natural than loading a classical table.

## 20. Key takeaways

- QAE estimates an unknown probability by encoding it as a Grover rotation angle and then estimating the corresponding phase.
- Standard Monte Carlo error scales as $O(N^{-1/2})$; ideal coherent QAE can achieve $O(1/M)$ error in its query model.
- The resulting query requirement is $O(1/\epsilon)$ rather than $O(1/\epsilon^2)$ for additive precision $\epsilon$.
- The advantage requires coherent state preparation, inverses, and reflections.
- Circuit depth and data-loading cost are central to practical comparisons.
- Modern QAE variants trade depth, sampling, adaptivity, and classical inference in different ways.

## References

1. G. Brassard, P. Høyer, M. Mosca, and A. Tapp, "Quantum Amplitude Amplification and Estimation." https://arxiv.org/abs/quant-ph/0005055
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
3. J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
