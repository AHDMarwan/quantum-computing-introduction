# PQC, VQC, QNN, and Related Terminology

## 1. Why terminology becomes confusing

Quantum machine learning inherited terminology from several communities at once:

- quantum algorithms,
- variational optimization,
- neural networks,
- quantum control,
- many-body physics.

As a result, the same circuit may be called a **PQC**, **variational circuit**, **QNN**, or **VQC** depending on what the authors want to emphasize.

The safest approach is to separate conceptual levels:

```math
\boxed{
\text{object}
\neq
\text{hypothesis family}
\neq
\text{training paradigm}
\neq
\text{task}
}
```

## 2. Learning objectives

After this chapter, you should be able to:

- define PQC, ansatz, VQA, VQC, and QNN at distinct levels,
- explain why VQC is an ambiguous acronym,
- distinguish a quantum circuit from the function class induced after measurement,
- distinguish architecture terminology from learning-task terminology,
- position VQE and QAOA relative to QML,
- identify when “QNN” is informative and when it is merely a broad label,
- and rewrite ambiguous QML descriptions into a precise ontology.

## 3. Parameterized Quantum Circuit (PQC)

A parameterized quantum circuit is a quantum circuit containing free parameters:

```math
U(\boldsymbol\theta).
```

For example,

```math
U(\theta_1,\theta_2)
=
\mathrm{CNOT}
\left[
R_y(\theta_1)\otimes R_z(\theta_2)
\right].
```

The definition says nothing about why the parameters exist.

A PQC may be used for:

- state preparation,
- quantum chemistry,
- optimal control,
- combinatorial optimization,
- machine learning,
- circuit compilation.

Therefore

```math
\text{PQC}
\not\equiv
\text{QML model}.
```

## 4. Ansatz

An ansatz is the family of candidate states or transformations defined by the parameterization.

For state preparation,

```math
\mathcal A
=
\left\{
U(\boldsymbol\theta)|\psi_0\rangle
:
\boldsymbol\theta\in\Theta
\right\}.
```

The PQC is a circuit description.

The ansatz is the represented family.

Two different circuit parameterizations can generate the same ansatz family, and one circuit may contain redundant parameters that do not increase the family dimension.

## 5. Variational Quantum Algorithm (VQA)

A VQA is a hybrid optimization framework:

```text
choose parameters
-> execute quantum model
-> estimate cost
-> classical update
-> repeat.
```

Mathematically,

```math
\boldsymbol\theta_{t+1}
=
\mathcal O
\left(
\boldsymbol\theta_t,
\widehat C(\boldsymbol\theta_t),
\widehat{\nabla C}(\boldsymbol\theta_t),
\ldots
\right).
```

A PQC can be a component inside a VQA, but the circuit alone is not the complete algorithm.

## 6. VQE and QAOA

VQE and QAOA are specific VQAs.

### VQE

Task:

```text
eigenvalue / ground-state estimation.
```

Objective:

```math
E(\theta)
=
\langle\psi(\theta)|H|\psi(\theta)\rangle.
```

### QAOA

Task:

```text
combinatorial optimization.
```

Architecture:

```math
\prod_{\ell=1}^{p}
e^{-i\beta_\ell H_M}
e^{-i\gamma_\ell H_C}.
```

Both use PQCs, but neither is automatically a machine-learning algorithm.

## 7. Variational Quantum Model

A **variational quantum model** is a useful neutral term for a trainable quantum map used inside an objective.

A general model can be written

```math
f_\theta(x)
=
\mathrm{Tr}
\left[
M
\mathcal E_{x,\theta}(\rho_0)
\right].
```

The trainable map may be:

- unitary,
- noisy,
- dissipative,
- measurement based,
- adaptive.

This term avoids implying a neural-network architecture when none has been specified.

## 8. Variational Quantum Circuit

Some papers use **VQC** to mean **Variational Quantum Circuit**.

In that usage, a VQC is essentially a trainable PQC embedded in a variational loop.

But because the same acronym is also widely used for **Variational Quantum Classifier**, the term is ambiguous.

This repository therefore avoids “VQC = variational quantum circuit” whenever possible.

## 9. Variational Quantum Classifier

Here, **VQC** is reserved for **Variational Quantum Classifier** when the classification role is explicit.

A binary classifier may use

```math
f_\theta(x)
=
\langle M\rangle_{x,\theta}
```

and predict

```math
\hat y
=
\mathrm{sign}[f_\theta(x)].
```

Or it may use a two-outcome POVM

```math
\{E_0,E_1\}
```

with

```math
p_\theta(y|x)
=
\mathrm{Tr}
\left[
E_y\rho_{x,\theta}
\right].
```

The term **classifier** refers to the task semantics, not merely to the circuit structure.

## 10. Quantum Neural Network (QNN)

“Quantum neural network” is the broadest and least standardized term in this cluster.

In many modern papers, it simply means a trainable parameterized quantum model.

In other work, QNN refers specifically to architectures with recognizable network-like structure, such as:

- layered local interactions,
- convolution and pooling,
- recurrent dynamics,
- graph message passing,
- dissipative feed-forward architectures.

Therefore a paper should define what **QNN** means operationally instead of relying on the acronym.

## 11. Why a PQC is not literally a classical neural network

A classical layer often has form

```math
h_{\ell+1}
=
\sigma(W_\ell h_\ell+b_\ell),
```

where $\sigma$ is a nonlinear activation.

A closed quantum circuit instead applies linear unitary transformations to state amplitudes:

```math
|\psi_{\ell+1}\rangle
=
U_\ell|\psi_\ell\rangle.
```

The classical input-output function can still be nonlinear because of:

- nonlinear data encoding in parameters,
- repeated feature injection,
- Born-rule probabilities,
- expectation values,
- classical postprocessing.

But the analogy “gate = neuron” should not be treated literally.

## 12. Where the effective nonlinearity comes from

Suppose

```math
|\phi(x)\rangle
=
R_y(x)|0\rangle.
```

Measuring $Z$ gives

```math
f(x)
=
\cos x.
```

The map

```math
x\mapsto\cos x
```

is nonlinear in the classical input even though the quantum state evolution is linear in Hilbert space.

Thus the effective classical function class arises from the composition

```text
classical parameterization
-> quantum linear evolution
-> quadratic Born rule / expectation
-> classical output.
```

## 13. Quantum circuit as hypothesis generator

A circuit alone does not specify the learned function.

Consider the same state family

```math
\rho_\theta(x).
```

Measuring $Z_1$ induces one function class:

```math
f_\theta^{(Z)}(x)
=
\mathrm{Tr}[Z_1\rho_\theta(x)].
```

Measuring $X_1$ induces another:

```math
f_\theta^{(X)}(x)
=
\mathrm{Tr}[X_1\rho_\theta(x)].
```

Therefore the effective hypothesis class depends jointly on:

```text
encoding
+ circuit/channel
+ measurement
+ postprocessing.
```

This is why calling the PQC itself “the model” can hide important structure.

## 14. Quantum Convolutional Neural Network (QCNN)

QCNN is more architecturally specific.

It refers to a multiscale structure built from local quantum convolution-like layers and pooling/coarse-graining operations.

The word “convolutional” is meaningful because locality, repeated local structure, and scale reduction are explicit architectural priors.

Thus QCNN is a more informative label than generic QNN.

## 15. Quantum Graph Neural Networks

Quantum graph models attempt to encode graph structure through:

- local node/edge interactions,
- permutation equivariance,
- message-passing-like quantum operations,
- graph-dependent Hamiltonians.

Again, the key point is that the architecture should expose why the “graph neural network” label is justified.

## 16. Dissipative QNNs

A trainable quantum network need not be unitary on the visible system.

A dissipative model can be written as layers of channels:

```math
\rho_{\ell+1}
=
\mathcal E_{\theta_\ell}(\rho_\ell).
```

Ancillas may be introduced and discarded between layers.

This can create a feed-forward architecture more structurally analogous to a classical neural network than a single global unitary PQC.

## 17. Quantum kernel model

A quantum kernel method is QML but generally should not be called a QNN.

Its quantum object may be a fixed feature map

```math
x\mapsto|\phi(x)\rangle,
```

and its learning algorithm can be a classical support-vector machine.

This provides an important counterexample:

```math
\text{QML}
\not\equiv
\text{QNN}.
```

## 18. Quantum Born machine

A quantum Born machine is a generative model where

```math
p_\theta(x)
=
|\langle x|\psi_\theta\rangle|^2.
```

It uses a PQC in many implementations, but calling it a classifier or VQC would be incorrect because the task is distribution learning.

Task semantics matter.

## 19. Model versus optimizer

Two papers can use exactly the same PQC and still define different learning algorithms because they use different:

- losses,
- optimizers,
- measurement allocation,
- data batching,
- initialization,
- regularization.

Thus model architecture and training algorithm must remain separate in terminology.

## 20. Model versus hardware

A PQC is also not a hardware platform.

The same abstract model could be compiled onto:

- superconducting qubits,
- trapped ions,
- neutral atoms,
- photonic qubits.

Hardware changes gate set, noise, connectivity, and physical resource cost, but not the abstract terminology level of the learning model.

## 21. Recommended terminology hierarchy

This repository uses:

```text
Quantum Machine Learning (QML)
= the research field

Parameterized Quantum Circuit (PQC)
= parameterized circuit object

Ansatz
= represented candidate family

Variational Quantum Algorithm (VQA)
= hybrid optimization framework

Variational quantum model
= trainable quantum model used in an objective

Variational Quantum Classifier (VQC)
= variational model whose task is classification

Quantum Neural Network (QNN)
= architecture-dependent umbrella term; define explicitly

QCNN / QGNN / dissipative QNN
= more specific architecture labels.
```

## 22. A four-layer ontology

A precise paper can be parsed into four levels.

### Level 1 — physical/computational object

```math
U(\theta)
```

or

```math
\mathcal E_\theta.
```

### Level 2 — representation family

```math
\mathcal H_\mathrm{model}
=
\{\rho_\theta\}_\theta.
```

### Level 3 — learning/optimization procedure

```math
\theta_*
=
\arg\min_\theta
\widehat{\mathcal L}(\theta).
```

### Level 4 — task

```text
classification
regression
generation
control
state learning
process learning.
```

Confusion usually occurs when one name is used across several levels.

## 23. Worked terminology example

Suppose we define

```math
U_\theta
=
\prod_{\ell}
U_\ell(\theta_\ell).
```

This is a **PQC**.

The set

```math
\left\{
U_\theta|0\rangle
\right\}_\theta
```

is the **ansatz**.

If we optimize

```math
\langle H\rangle_\theta
```

to estimate molecular ground energy, the complete algorithm is **VQE**.

If instead data $x$ are encoded and we optimize cross-entropy for labels, the same PQC becomes part of a **variational quantum classifier**.

The mathematical circuit can remain the same while the algorithmic identity changes.

## 24. Why terminology precision matters for literature search

Searching only for “QNN” can miss relevant work described as:

- variational quantum circuits,
- parameterized quantum circuits,
- quantum circuit learning,
- quantum classifiers,
- trainable quantum models.

Conversely, searching “PQC” retrieves work unrelated to machine learning.

A good prior-art search therefore uses several terminology families and then classifies results by function rather than title alone.

## 25. Why terminology precision matters for novelty

A proposed “new QNN architecture” may already exist under a different label.

To assess novelty, compare the actual tuple

```math
(
\text{data access},
\text{state/channel family},
\text{measurement},
\text{loss},
\text{training rule}
)
```

rather than only architecture names.

This is particularly important in fast-moving QML literature.

## 26. Common misconceptions

### “PQC means quantum neural network.”

No. PQC is task agnostic.

### “VQC always means variational quantum classifier.”

No. The acronym is ambiguous across papers; expand it on first use.

### “Any trainable quantum circuit is naturally a neural network.”

That is a convention in some literature, not a unique mathematical definition.

### “VQE and QAOA are QML because they train parameters.”

Parameter optimization alone does not make an algorithm machine learning.

### “The circuit uniquely determines the hypothesis class.”

Measurement, encoding, and classical postprocessing also matter.

## 27. Terminology audit template

When reading a paper, fill in:

```text
Author's term:
Actual quantum object:
Input/data dependence:
Parameterized variables:
Output measurement:
Objective/loss:
Training algorithm:
Task:
Closest neutral description:
```

This often resolves terminology ambiguity immediately.

## 28. Exercises

### Conceptual

1. Explain why VQE uses a PQC but is not automatically QML.
2. Give an example where two different measurements turn the same state family into different hypothesis classes.
3. Why is “QNN” less mathematically precise than “PQC”?
4. Distinguish a model architecture from its optimizer.

### Computational

5. For

```math
|\psi_\theta(x)\rangle
=
R_y(\theta)R_z(x)|+\rangle,
```

write two scalar models obtained by measuring $X$ and $Z$ respectively.
6. Show that a one-qubit $R_y(\theta)$ ansatz generates all pure qubit states only on one great circle, not the full Bloch sphere.
7. Given a binary two-outcome POVM, write the corresponding classifier probabilities.
8. For a Born machine, explain why the output is a probability distribution rather than a deterministic scalar prediction.

### Research-oriented

9. Find three papers using the word QNN and classify what mathematical object each actually trains.
10. Propose a formal ontology that distinguishes circuit, channel, measurement, loss, and task for QML literature databases.
11. How could terminology ambiguity create a false novelty claim?
12. Rewrite a hypothetical phrase “we propose a novel QNN” into a scientifically precise claim specifying the actual architectural novelty.

## 29. Key takeaways

- PQC, ansatz, VQA, VQC, and QNN describe different conceptual levels.
- VQC is an ambiguous acronym and should be expanded explicitly.
- QNN is an umbrella architecture term whose meaning varies across literature.
- The effective learning model depends jointly on encoding, quantum transformation, measurement, and postprocessing.
- VQE and QAOA are variational algorithms but not QML by definition.
- Precise terminology is important for comparison, literature search, and novelty assessment.

## References

1. M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
2. K. Mitarai et al., "Quantum circuit learning," *Physical Review A* 98, 032309 (2018). https://doi.org/10.1103/PhysRevA.98.032309
3. J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
4. [Repository Terminology Map](../08-reference/terminology-map.md)
