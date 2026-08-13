# Variational Quantum Algorithms

Variational quantum algorithms (VQAs) combine parameterized quantum computations with classical optimization. They form an **algorithmic paradigm**, not a single algorithm and not a synonym for quantum machine learning.

This section is the bridge between canonical quantum algorithms and QML because it introduces trainable circuits, measured objectives, gradients, finite-shot estimation, and classical optimization.

## Recommended learning path

```text
parameterized circuit
→ ansatz / candidate family
→ hybrid variational loop
→ VQE
→ QAOA
→ gradients and measurement cost
→ trainability and barren plateaus
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
= family of candidate states or transformations

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

See also the [Terminology Map](../08-reference/terminology-map.md).

## How the chapters are organized

Each variational method is studied through the following layers:

```text
model family
→ objective
→ quantum measurement
→ classical optimizer
→ gradient information
→ measurement cost
→ noise
→ trainability
→ practical limitations
```

This helps explain why a shallow circuit is not automatically a cheap algorithm: training may require many circuit evaluations and many measurement shots.

## Understanding total training cost

A rough VQA training cost often has the form

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

Depending on the method, additional costs can come from state preparation, observable grouping, gradient estimation, error mitigation, compilation, and classical optimization.

The point is not to memorize this expression, but to recognize that variational algorithms are **repeated hybrid procedures**, not one-shot circuits.

## Four common failure modes

When a VQA performs poorly, it helps to separate several possibilities.

### 1. Representation failure

The ansatz cannot represent a sufficiently good solution.

### 2. Optimization failure

A good solution exists, but the optimizer does not find it.

### 3. Measurement failure

The objective or gradient cannot be estimated accurately enough with the available number of shots.

### 4. Hardware failure

Noise and device imperfections distort the ideal circuit behavior.

These mechanisms can interact, but the distinction is useful for learning how VQAs behave.

## Learning goals

After completing this section, you should be able to:

- distinguish PQCs, ansätze, VQAs, VQE, QAOA, and variational QML,
- explain what a trainable quantum circuit represents,
- derive the variational upper bound for ground-state energy,
- describe the hybrid quantum-classical optimization loop,
- reconstruct VQE energies from Pauli expectation values,
- explain why measurement cost matters in VQE,
- derive the MaxCut QAOA cost Hamiltonian,
- explain the roles of cost and mixer Hamiltonians,
- distinguish QAOA from quantum annealing,
- derive the parameter-shift rule in the common Pauli-rotation setting,
- compare several gradient and derivative-free optimization strategies,
- distinguish finite-shot noise from hardware bias,
- define barren plateaus and explain why they make training difficult,
- and describe common strategies used to improve trainability.

## Variational algorithm comparison map

| Concept | Object being optimized | Main quantum operation | Main learning point |
|---|---|---|---|
| Generic VQA | $C(\boldsymbol\theta)$ | PQC + measurements | Hybrid optimization loop |
| VQE | Energy expectation | State ansatz + Pauli measurements | Variational eigensolving |
| QAOA | Discrete objective expectation | Alternating cost/mixer layers | Structured variational optimization |
| Gradient training | Derivative estimates | Shifted or perturbed circuits | Training requires repeated measurements |
| Natural gradient | Geometry-aware update | Cost + metric estimation | Parameter space has nontrivial geometry |
| Barren plateaus | Gradient statistics | Gradient probes | Expressivity and trainability can conflict |

## A study checklist

When learning a new VQA, ask:

1. What is parameterized?
2. What family of states or operations can the ansatz represent?
3. What quantity is being minimized or maximized?
4. What measurements are required to estimate it?
5. How are parameters updated?
6. How many circuit evaluations are needed per update?
7. What kinds of noise affect the result?
8. What happens as the number of qubits or circuit depth grows?

## Connection to QML

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

Training such a model reuses the same ideas developed here:

```text
data encoding
+ PQC architecture
+ measurement
+ finite-shot estimation
+ gradient estimation
+ classical optimization
```

Understanding VQAs first makes VQCs and QNNs much easier to interpret later.

## Suggested study method

For each chapter:

1. Identify the mathematical object being optimized.
2. Write the ansatz explicitly.
3. Derive the measured objective.
4. Follow one optimizer step from quantum measurement to classical update.
5. Distinguish statistical measurement noise from device noise.
6. Work through at least one explicit example.
7. Complete the conceptual and computational exercises before moving on.

## Core references

- M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
- J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New Journal of Physics* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
- A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nature Communications* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
- E. Farhi, J. Goldstone, and S. Gutmann, "A Quantum Approximate Optimization Algorithm." https://arxiv.org/abs/1411.4028
- J. R. McClean et al., "Barren plateaus in quantum neural network training landscapes," *Nature Communications* 9, 4812 (2018). https://doi.org/10.1038/s41467-018-07090-4
