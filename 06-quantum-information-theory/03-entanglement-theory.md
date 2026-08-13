# Entanglement Theory

## 1. From a definition to an operational theory

For a pure bipartite state, entanglement means nonfactorizability. For mixed states, the situation is richer because classical mixtures can produce correlations without quantum entanglement.

A bipartite mixed state is **separable** if it can be written

```math
\rho_{AB}
=
\sum_j p_j
\rho_A^{(j)}
\otimes
\rho_B^{(j)},
```

where

```math
p_j\ge0,
\qquad
\sum_jp_j=1.
```

Any state that cannot be represented this way is entangled.

Entanglement theory asks not only whether entanglement is present, but also:

- how much is present,
- whether it can be detected efficiently,
- whether it can be converted into another useful form,
- and what operational tasks it enables.

## 2. Learning objectives

After this chapter, you should be able to:

- characterize bipartite pure-state entanglement using Schmidt coefficients,
- compute entanglement entropy,
- distinguish entanglement from classical correlation and Bell nonlocality,
- define separability for mixed states,
- use the partial-transpose criterion in low dimensions,
- explain why mixed-state entanglement has many inequivalent measures,
- define LOCC as a restricted operational class,
- explain distillation and entanglement cost,
- and evaluate claims that entanglement alone guarantees quantum computational or learning advantage.

## 3. Schmidt decomposition

Every bipartite pure state can be written

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
\sum_k\lambda_k=1.
```

The integer $r$ is the Schmidt rank.

The state is a product state exactly when

```math
r=1.
```

If

```math
r>1,
```

the state is entangled.

## 4. Reduced-state spectra

Tracing out subsystem $B$ gives

```math
\rho_A
=
\sum_k\lambda_k
|u_k\rangle\langle u_k|.
```

Similarly,

```math
\rho_B
=
\sum_k\lambda_k
|v_k\rangle\langle v_k|.
```

Therefore the nonzero spectra of $\rho_A$ and $\rho_B$ are identical.

This is why pure-state entanglement can be quantified using the entropy of either subsystem.

## 5. Entanglement entropy

For a bipartite pure state,

```math
E(|\psi\rangle)
=
S(\rho_A)
=
S(\rho_B).
```

Using Schmidt coefficients,

```math
E(|\psi\rangle)
=
-\sum_k
\lambda_k\log\lambda_k.
```

It vanishes exactly for product states.

For a maximally entangled state of local dimension $d$,

```math
\lambda_k=\frac1d,
```

and

```math
E=\log d.
```

## 6. Worked example: Bell pair

For

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2},
```

the Schmidt coefficients are

```math
\lambda_1=\lambda_2=\frac12.
```

Therefore

```math
E(|\Phi^+\rangle)
=
-2\frac12\log_2\frac12
=1
```

ebit.

The reduced states are

```math
\rho_A=\rho_B=\frac I2.
```

## 7. Classical correlation is not entanglement

Consider

```math
\rho_{
\mathrm{cc}}
=
\frac12|00\rangle\langle00|
+
\frac12|11\rangle\langle11|.
```

This state has strong correlations: measuring one qubit in the computational basis predicts the other.

But it is explicitly a convex mixture of product states, so it is separable.

Thus

```math
\text{correlation}
\not\Rightarrow
\text{entanglement}.
```

Quantum mutual information counts both classical and quantum correlations.

## 8. Mixed-state entanglement

For a mixed state, there is no Schmidt decomposition of the state itself that completely solves the entanglement problem.

The separability question is whether there exists **any** decomposition

```math
\rho_{AB}
=
\sum_jp_j
\rho_A^{(j)}\otimes\rho_B^{(j)}.
```

This is difficult because density-matrix decompositions are highly nonunique.

A representation that looks entangled does not prove the state is entangled; one must rule out all separable decompositions.

## 9. Partial transpose

In a product basis, write

```math
\rho
=
\sum_{i,j,k,l}
\rho_{ij,kl}
|i\rangle\langle k|
\otimes
|j\rangle\langle l|.
```

Partial transpose on subsystem $B$ gives

```math
\rho^{T_B}
=
\sum_{i,j,k,l}
\rho_{ij,kl}
|i\rangle\langle k|
\otimes
|l\rangle\langle j|.
```

Every separable state has

```math
\rho^{T_B}\succeq0.
```

This is the PPT condition.

## 10. PPT criterion

If

```math
\rho^{T_B}
```

has a negative eigenvalue, the state is definitely entangled.

For bipartite dimensions

```math
2\times2
```

and

```math
2\times3,
```

PPT is also sufficient for separability.

In larger dimensions, there exist entangled states with positive partial transpose.

These are examples of bound entanglement.

## 11. Worked example: Bell-state partial transpose

The Bell-state density operator is

```math
\rho_{\Phi^+}
=
\frac12
\left(
|00\rangle\langle00|
+|00\rangle\langle11|
+|11\rangle\langle00|
+|11\rangle\langle11|
\right).
```

After partial transpose on $B$,

```math
\rho_{\Phi^+}^{T_B}
=
\frac12
\left(
|00\rangle\langle00|
+|01\rangle\langle10|
+|10\rangle\langle01|
+|11\rangle\langle11|
\right).
```

Its eigenvalues include

```math
-\frac12,
```

so the Bell state is detected as entangled.

## 12. Negativity

The negative spectrum of the partial transpose motivates the **negativity**:

```math
\mathcal N(\rho)
=
\frac{
\|\rho^{T_B}\|_1-1
}{2}.
```

Negativity is easy to define and useful computationally, but it is not the unique measure of mixed-state entanglement.

Different measures capture different operational tasks.

## 13. Entanglement of formation

The entanglement of formation asks for the least average pure-state entanglement needed in an ensemble decomposition:

```math
E_F(\rho)
=
\inf_{\{p_j,|\psi_j\rangle\}}
\sum_jp_j
E(|\psi_j\rangle),
```

where

```math
\rho
=
\sum_jp_j
|\psi_j\rangle\langle\psi_j|.
```

It is a convex-roof construction.

This shows how mixed-state resource quantification can require optimization over all decompositions.

## 14. Distillable entanglement

Distillable entanglement asks how many nearly perfect Bell pairs can be extracted asymptotically from many copies of a noisy entangled state using allowed local operations and classical communication.

Schematically,

```text
many noisy entangled pairs
-> LOCC protocol
-> fewer high-quality Bell pairs.
```

This is an operational conversion rate, not merely a static state property.

## 15. Entanglement cost

The reverse question asks how many Bell pairs are needed asymptotically to prepare copies of a target entangled state under LOCC.

Thus entanglement theory naturally studies resource conversion rates:

```text
standard resource
<->
target state.
```

For general mixed states, formation cost and distillable entanglement can differ.

This irreversibility is one reason mixed-state entanglement theory is richer than pure-state theory.

## 16. LOCC

LOCC stands for **local operations and classical communication**.

Alice and Bob may:

- perform arbitrary local quantum operations,
- measure locally,
- communicate classical outcomes,
- condition later local operations on those messages.

But they cannot directly apply a joint entangling gate across their separated systems.

LOCC cannot create entanglement from a separable input.

This makes entanglement a resource relative to the restriction to LOCC.

## 17. Entanglement monotones

A reasonable entanglement measure should not increase under free operations.

Schematically,

```math
E(\Lambda_{\mathrm{LOCC}}(\rho))
\le
E(\rho)
```

for deterministic LOCC transformations.

More refined monotonicity conditions apply to probabilistic branches and averages.

This connects entanglement theory directly to general quantum resource theories.

## 18. Bell nonlocality

Entanglement and Bell nonlocality are related but not identical.

Bell nonlocality concerns whether observed correlations admit a local hidden-variable model.

Every Bell-nonlocal state is entangled, but not every entangled mixed state violates a chosen Bell inequality.

Thus

```math
\text{Bell nonlocality}
\subsetneq
\text{entanglement}
```

at the level of general state sets, with details depending on measurement scenarios.

## 19. Entanglement and teleportation

Shared entanglement enables teleportation, but operational usefulness depends on the state's quality and protocol.

This is a useful reminder that resource presence and task performance are different questions.

A state can be entangled yet be poor for a specific protocol without preprocessing.

## 20. Multipartite entanglement

For three or more parties, entanglement structure becomes substantially richer.

States such as GHZ and W are not equivalent under simple local transformations:

```math
|\mathrm{GHZ}\rangle
=
\frac{|000\rangle+|111\rangle}{\sqrt2},
```

```math
|W\rangle
=
\frac{|001\rangle+|010\rangle+|100\rangle}{\sqrt3}.
```

There is no single Schmidt decomposition that classifies all multipartite pure states.

This complexity matters in quantum networks, many-body physics, and QML architecture analysis.

## 21. Entanglement in many-body systems

Entanglement structure helps characterize:

- quantum phases,
- critical systems,
- thermalization,
- tensor-network simulability,
- information propagation.

For one-dimensional gapped systems, area-law entanglement often supports efficient tensor-network approximations.

Therefore high Hilbert-space dimension alone does not determine classical simulation difficulty; entanglement structure is one major factor.

## 22. Entanglement in quantum computing

Entanglement is necessary for some forms of quantum computational complexity, but the simple statement

```math
\text{more entanglement}
\Rightarrow
\text{more speedup}
```

is false.

Some highly entangled states remain classically simulable under special structure, while useful algorithms may exploit other resources such as magic, interference, or oracle access.

Entanglement is one resource among several.

## 23. Entanglement in QML

QML papers often correlate entanglement with expressivity.

But a useful learning model must balance:

```text
correlation capacity
trainability
measurement accessibility
classical simulability
inductive bias.
```

An ansatz producing generic high entanglement may become difficult to train through concentration effects.

Conversely, a low-entanglement structured ansatz may generalize well on a local physical task.

## 24. Common misconceptions

### “Correlation means entanglement.”

No. Separable mixed states can have strong classical correlations.

### “Entropy of a mixed state's subsystem directly measures entanglement.”

Not generally. For mixed states, subsystem entropy includes multiple sources of uncertainty.

### “PPT always proves separability.”

Only in low-dimensional bipartite cases such as $2\times2$ and $2\times3$.

### “Any entangled state violates a Bell inequality.”

Not necessarily in a given Bell scenario.

### “More entanglement automatically means more quantum advantage.”

No. Operational task and competing resources matter.

## 25. Exercises

### Conceptual

1. Why does Schmidt rank classify bipartite pure-state separability?
2. Explain why the classically correlated state $\rho_{\mathrm{cc}}$ is separable.
3. What operational restriction makes entanglement a resource under LOCC?
4. Why can different mixed-state entanglement measures disagree numerically without contradiction?

### Computational

5. Compute the entanglement entropy of

```math
|\psi\rangle
=
\sqrt{3/4}|00\rangle
+
\sqrt{1/4}|11\rangle.
```
6. Compute the partial transpose of $\rho_{\mathrm{cc}}$ and verify that it is positive.
7. Compute the negativity of a Bell state.
8. Determine the Schmidt rank of

```math
\frac{|00\rangle+|01\rangle+|10\rangle+|11\rangle}{2}.
```

### Research-oriented

9. A QML paper claims advantage because its trained states have high entanglement entropy. What additional evidence is required?
10. How would you compare entanglement structure between a trainable PQC and a tensor-network classical baseline?
11. Could entanglement serve as an inductive bias rather than merely a complexity resource? Formulate a task where this distinction matters.
12. Which learning tasks might naturally treat entanglement distillation itself as an optimization target?

## 26. Key takeaways

- Bipartite pure-state entanglement is completely characterized by Schmidt coefficients.
- Entanglement entropy is the unique standard pure-state asymptotic measure under common assumptions, but mixed-state entanglement requires multiple measures.
- Separable states can still contain classical correlation.
- PPT is a powerful low-dimensional separability criterion but is not universally sufficient.
- LOCC defines an operational restriction under which entanglement becomes a resource.
- Distillation and formation reveal entanglement as a convertible resource, not just a static label.
- Entanglement alone is not a certificate of computational or learning advantage.

## References

1. R. Horodecki et al., "Quantum entanglement," *Reviews of Modern Physics* 81, 865 (2009). https://doi.org/10.1103/RevModPhys.81.865
2. M. B. Plenio and S. Virmani, "An introduction to entanglement measures," *Quantum Information and Computation* 7, 1–51 (2007). https://arxiv.org/abs/quant-ph/0504163
3. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
