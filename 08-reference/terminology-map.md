# Terminology Map

Quantum-computing and quantum-machine-learning terminology is not perfectly standardized across the literature. This repository therefore adopts an explicit hierarchy that separates **objects**, **representation families**, **optimization paradigms**, and **tasks**.

## Core Distinction

```text
Computational object
        │
        ▼
Parameterized Quantum Circuit (PQC)
        │
        ├── may instantiate an ansatz
        │
        ├── may be optimized inside a VQA
        │
        └── may be used as a QML model
```

The guiding principle is

$$
\boxed{
\text{object}
\neq
\text{representation family}
\neq
\text{optimization paradigm}
\neq
\text{task}
}
$$

## Parameterized Quantum Circuit (PQC)

A **parameterized quantum circuit** is a quantum circuit containing free parameters:

$$
U(\boldsymbol\theta).
$$

The term says nothing, by itself, about the purpose of the circuit or how its parameters are chosen.

A PQC may be used in quantum chemistry, combinatorial optimization, machine learning, quantum control, state preparation, or other tasks.

## Ansatz

An **ansatz** is a chosen family of candidate states or transformations intended to contain, or approximate, solutions of a problem.

For a state ansatz,

$$
\mathcal A
=
\left\{
|\psi(\boldsymbol\theta)\rangle
:
\boldsymbol\theta\in\Theta
\right\}.
$$

A PQC is one common way to implement an ansatz, but the two terms describe different conceptual levels.

## Variational Quantum Algorithm (VQA)

A **variational quantum algorithm** is a hybrid optimization framework in which a parameterized quantum computation is evaluated on quantum hardware and a classical optimization procedure updates its parameters.

A generic loop is

$$
\boldsymbol\theta_t
\rightarrow
U(\boldsymbol\theta_t)
\rightarrow
C(\boldsymbol\theta_t)
\rightarrow
\text{classical optimizer}
\rightarrow
\boldsymbol\theta_{t+1}.
$$

Thus, a PQC may be a component of a VQA, but a PQC is not itself a VQA.

## Variational Quantum Eigensolver (VQE)

**VQE** is a specific VQA designed primarily for eigenvalue problems, especially ground-state-energy estimation.

Its objective has the form

$$
E(\boldsymbol\theta)
=
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle.
$$

VQE is therefore an algorithmic application of a variational ansatz, not a synonym for PQC.

## Quantum Approximate Optimization Algorithm (QAOA)

**QAOA** is a structured variational algorithm for combinatorial optimization. A depth-$p$ QAOA state typically has the form

$$
|\psi(\boldsymbol\gamma,\boldsymbol\beta)\rangle
=
\prod_{j=1}^{p}
 e^{-i\beta_j H_M}
 e^{-i\gamma_j H_C}
|+\rangle^{\otimes n}.
$$

Its circuit is parameterized, so it is a PQC, while the complete procedure is a particular VQA.

## Variational Quantum Circuit (VQC)

The acronym **VQC** is ambiguous in the literature. It may mean:

- **Variational Quantum Circuit**, or
- **Variational Quantum Classifier**.

To avoid ambiguity, this repository uses:

- **PQC** for the circuit object $U(\boldsymbol\theta)$,
- **variational quantum model** for a trainable model more generally,
- **variational quantum classifier** when the task is explicitly classification.

The acronym **VQC** should therefore be expanded on first use whenever it appears.

## Quantum Neural Network (QNN)

**Quantum neural network** is an umbrella term whose usage varies substantially across papers. In many modern QML works it refers to a trainable parameterized quantum model, but not every PQC has a meaningful neural-network interpretation.

This repository uses **QNN** only when the neural or layered architectural interpretation is relevant. Otherwise, **parameterized quantum model** or **variational quantum model** is preferred.

## Quantum Machine Learning (QML)

**Quantum machine learning** is a research field, not a single circuit family or optimization algorithm.

It includes, among other areas:

- variational quantum learning,
- quantum kernel methods,
- quantum generative models,
- quantum reservoir computing,
- quantum reinforcement learning,
- quantum learning theory,
- learning from quantum states, channels, Hamiltonians, and processes.

Therefore,

$$
\mathrm{QML}\neq\mathrm{PQC}\neq\mathrm{VQA}.
$$

These concepts overlap, but they are not interchangeable.

## Relationship Summary

```text
PQC
│
├── can implement an Ansatz
│
├── can be used inside a VQA
│   ├── VQE
│   ├── QAOA
│   └── other VQAs
│
└── can be used inside QML
    ├── variational classifier
    ├── regressor
    ├── QNN
    ├── generative model
    └── other parameterized quantum models

QML also includes methods that need not use trainable PQCs,
for example quantum kernel methods.
```

## Terminology Standardization

A formal vocabulary standard for quantum computing exists in **ISO/IEC 4879:2024, Information technology — Quantum computing — Vocabulary**. The standard defines terms used broadly across quantum computing, but research-level QML terminology remains less uniform, especially for terms such as PQC, VQC, ansatz, and QNN.

## References

1. ISO/IEC 4879:2024, *Information technology — Quantum computing — Vocabulary*. https://www.iso.org/standard/80432.html
2. John Preskill, *Quantum Computation Lecture Notes*, California Institute of Technology. https://www.preskill.caltech.edu/ph229/
3. John Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
