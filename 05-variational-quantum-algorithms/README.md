# Variational Quantum Algorithms

Variational quantum algorithms (VQAs) combine parameterized quantum computations with classical optimization. They form an **algorithmic paradigm**, not a single algorithm and not a synonym for quantum machine learning.

This section is the bridge between canonical quantum algorithms and QML because it introduces the trainable circuit, noisy objective, measurement, and optimization machinery reused throughout variational quantum learning.

## Recommended learning path

```text
parameterized circuit
-> ansatz / hypothesis family
-> hybrid variational loop
-> VQE
-> QAOA
-> gradient and measurement estimation
-> trainability and barren plateaus
```

## Contents

1. [Parameterized Quantum Circuits and Ansätze](01-pqc-and-ansatz.md)
2. [Variational Principle and Hybrid Loop](02-variational-principle.md)
3. [Variational Quantum Eigensolver](03-vqe.md)
4. [Quantum Approximate Optimization Algorithm](04-qaoa.md)
5. [Optimization, Gradients, and Measurement Cost](05-optimization-and-gradients.md)
6. [Barren Plateaus and Trainability](06-barren-plateaus.md)

## Terminology hierarchy

The repository uses the following distinction:

```text
PQC
= parameterized circuit object

Ansatz
= family of candidate states / transformations

VQA
= hybrid optimization framework

VQE / QAOA
= specific variational algorithms
```

Therefore

```math
\boxed{
\text{PQC}
\neq
\text{ansatz}
\neq
\text{VQA}
}
```

although a PQC commonly implements an ansatz inside a VQA.

See also [Terminology Map](../08-reference/terminology-map.md).

## Phase 4 chapter standard

The section analyzes each variational method through the following layers:

```text
model family
-> objective
-> quantum estimator
-> classical optimizer
-> measurement cost
-> gradient information
-> trainability
-> noise
-> total resource accounting
```

The goal is to avoid the common shortcut

```text
short quantum circuit
therefore
cheap quantum algorithm
```

which is generally false for hybrid optimization.

## The total-training-cost principle

A rough VQA training cost often has multiplicative structure:

```math
C_{\mathrm{train}}
\sim
N_{\mathrm{iter}}
\times
N_{\mathrm{settings/iter}}
\times
N_{\mathrm{shots/setting}}
\times
C_{\mathrm{circuit}}.
```

Depending on the algorithm, one must additionally count:

- state preparation,
- observable grouping,
- gradient estimation,
- error mitigation,
- classical optimization,
- device communication latency,
- calibration and compilation.

This is the relevant scale for comparing practical variational workflows.

## Four distinct failure modes

When a VQA performs poorly, ask which layer failed.

### 1. Representation failure

The ansatz does not contain a sufficiently good solution.

```math
\text{target}
\notin
\mathcal A
```

or cannot be approximated well enough.

### 2. Optimization failure

A good solution exists in the ansatz, but the optimizer fails to find it.

Possible causes include local structure, poor initialization, noisy gradients, or concentration.

### 3. Measurement failure

The relevant objective or gradient cannot be estimated with affordable statistical precision.

### 4. Hardware failure

Noise biases or suppresses the information produced by the ideal circuit.

These mechanisms interact, but separating them is essential for diagnosis.

## Learning goals

After completing this section, you should be able to:

- distinguish PQCs, ansätze, VQAs, VQE, QAOA, and variational QML,
- analyze circuit architecture using expressibility, symmetry, locality, and inductive bias,
- derive the variational upper bound for ground-state energy,
- decompose VQA error into representation, optimization, sampling, and hardware components,
- reconstruct VQE energies from Pauli expectation values,
- identify measurement variance and shot allocation as algorithmic resources,
- derive the MaxCut QAOA cost Hamiltonian,
- explain cost and mixer evolution geometrically and operationally,
- distinguish QAOA from quantum annealing,
- derive the parameter-shift gradient rule,
- estimate full-gradient measurement cost,
- compare parameter shift, SPSA, derivative-free methods, and quantum natural gradient,
- distinguish sampling noise from hardware bias,
- define barren plateaus through system-size gradient scaling,
- distinguish concentration, symmetry, light-cone, redundancy, and noise mechanisms for small gradients,
- and evaluate trainability mitigation through scaling evidence rather than small-system demonstrations.

## Variational algorithm comparison map

| Concept | Object being optimized | Main quantum operation | Main practical bottleneck |
|---|---|---|---|
| Generic VQA | $C(\boldsymbol\theta)$ | PQC + measurements | repeated noisy optimization |
| VQE | energy expectation | state ansatz + Pauli measurements | ansatz + measurement + optimization |
| QAOA | discrete objective expectation | alternating cost/mixer layers | parameter training + depth + classical competition |
| Gradient training | derivative estimates | shifted / perturbed circuits | shots × parameters × iterations |
| Natural gradient | geometry-aware updates | cost + metric estimation | metric measurement / inversion |
| Barren-plateau analysis | gradient distribution | repeated gradient probes | resolving exponentially weak signal |

## A recurring audit checklist

For any variational quantum paper, ask:

1. What exactly is parameterized?
2. What family does the ansatz represent?
3. Which symmetries or physical constraints are preserved?
4. How many trainable parameters are there?
5. How many quantum circuit evaluations are required per optimizer step?
6. How many measurements are required per circuit setting?
7. Is the cost local or global?
8. How do gradients scale with system size?
9. Is initialization specified?
10. What optimizer is used, and with what total evaluation budget?
11. How is hardware noise separated from finite-shot noise?
12. What classical baseline is relevant?
13. Is performance shown only at fixed small size, or is scaling studied?
14. Is the claimed advantage computational, representational, or merely empirical?

## Why this matters for QML

A common variational QML model has the form

```math
f_{\boldsymbol\theta}(x)
=
\mathrm{Tr}
\left[
M
U(x,\boldsymbol\theta)
\rho_0
U^\dagger(x,\boldsymbol\theta)
\right].
```

Training then introduces all of the VQA complications simultaneously:

```text
data encoding
+ PQC architecture
+ measurement
+ finite-shot loss estimation
+ gradient estimation
+ classical optimization
+ generalization
```

Therefore the VQA section supplies the optimization language needed to analyze VQCs, QNNs, QCNNs, and other trainable quantum models rigorously.

## Suggested study method

For each chapter:

1. Identify the mathematical object being optimized.
2. Write the hypothesis family explicitly.
3. Derive the measured objective.
4. Count how many circuit executions one optimizer iteration requires.
5. Identify which errors are statistical and which are systematic.
6. Ask whether trainability is demonstrated as a scaling statement.
7. Complete at least one resource-accounting exercise.
8. Treat every “quantum advantage” statement as incomplete until the classical baseline and total training budget are explicit.

## Core references

- M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
- J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New Journal of Physics* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
- A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nature Communications* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
- E. Farhi, J. Goldstone, and S. Gutmann, "A Quantum Approximate Optimization Algorithm." https://arxiv.org/abs/1411.4028
- J. R. McClean et al., "Barren plateaus in quantum neural network training landscapes," *Nature Communications* 9, 4812 (2018). https://doi.org/10.1038/s41467-018-07090-4
