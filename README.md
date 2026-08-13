# Quantum Computing Introduction

A structured educational introduction to **quantum information science (QIS)**, **quantum computing**, and **quantum machine learning (QML)**.

The goal of this repository is to make the field easier to learn without flattening the mathematics. It separates mathematical foundations, computational models, hardware platforms, algorithms, variational methods, quantum information theory, and QML so that the relationships between them remain clear.

> **Format:** all scientific content is stored in Markdown (`.md`) files and rendered directly on GitHub.
>
> **Web entry point:** [`index.html`](index.html) provides a lightweight landing page for the repository and can be published directly with GitHub Pages.

## Who is this for?

This repository is intended for students, software engineers, physicists, mathematicians, and curious readers who want a coherent path into quantum computing.

You do **not** need prior knowledge of quantum computing. Basic familiarity with linear algebra, complex numbers, probability, and introductory calculus is helpful. When a more advanced concept is needed, the relevant chapter introduces the notation before using it.

## How to use this repository

The recommended path is

```text
foundations
→ computational models
→ hardware
→ canonical algorithms
→ variational algorithms
→ quantum information theory
→ quantum machine learning
→ reference / terminology
```

The sections can also be used independently as a reference.

Most chapters are organized around the same learning pattern:

```text
motivation
→ learning objectives
→ intuition
→ mathematical formulation
→ derivations
→ worked examples
→ common misconceptions
→ exercises
→ key takeaways
```

Some advanced chapters also discuss limitations, resource requirements, and comparisons between methods. These sections are included to help readers interpret the subject correctly, not as a prerequisite for beginning the course.

## 1. Foundations

Start here for the mathematical language of quantum information.

- [Section index](01-foundations/README.md)
- [Quantum Information Science: The Big Picture](01-foundations/01-quantum-information-science.md)
- [Classical vs Quantum Information](01-foundations/02-classical-vs-quantum-information.md)
- [Qubits and Hilbert Spaces](01-foundations/03-qubits-and-hilbert-spaces.md)
- [The Bloch Sphere](01-foundations/04-bloch-sphere.md)
- [Composite Systems and Tensor Products](01-foundations/05-composite-systems.md)
- [Entanglement](01-foundations/06-entanglement.md)
- [Density Matrices and Mixed States](01-foundations/07-density-matrices.md)
- [Measurements and POVMs](01-foundations/08-measurements-and-povms.md)

## 2. Computational Models of Quantum Computing

Learn the main ways in which quantum computation can be organized mathematically.

- [Section index](02-quantum-computing/README.md)
- [Gate-Based / Circuit Model](02-quantum-computing/01-gate-model.md)
- [Adiabatic Quantum Computing](02-quantum-computing/02-adiabatic-computing.md)
- [Quantum Annealing](02-quantum-computing/03-quantum-annealing.md)
- [Analog Quantum Computing and Simulation](02-quantum-computing/04-analog-quantum-computing.md)
- [Measurement-Based Quantum Computing](02-quantum-computing/05-measurement-based-qc.md)
- [Continuous-Variable Quantum Computing](02-quantum-computing/06-continuous-variable-qc.md)

## 3. Hardware Platforms

See how abstract quantum information is implemented physically.

- [Section index](03-hardware/README.md)
- [Superconducting Qubits](03-hardware/01-superconducting-qubits.md)
- [Trapped Ions](03-hardware/02-trapped-ions.md)
- [Neutral Atoms](03-hardware/03-neutral-atoms.md)
- [Photonics](03-hardware/04-photonics.md)
- [Semiconductor and Spin Qubits](03-hardware/05-spin-qubits.md)
- [Topological Approaches](03-hardware/06-topological-approaches.md)

## 4. Quantum Algorithms

Study canonical examples of how interference, phase, Fourier structure, and coherent access are used computationally.

- [Section index](04-quantum-algorithms/README.md)
- [Deutsch–Jozsa](04-quantum-algorithms/01-deutsch-jozsa.md)
- [Grover Search and Amplitude Amplification](04-quantum-algorithms/02-grover.md)
- [Quantum Phase Estimation](04-quantum-algorithms/03-phase-estimation.md)
- [Shor's Algorithm](04-quantum-algorithms/04-shor.md)
- [Quantum Simulation](04-quantum-algorithms/05-quantum-simulation.md)
- [Amplitude Estimation](04-quantum-algorithms/06-amplitude-estimation.md)

## 5. Variational Quantum Algorithms

Learn how parameterized circuits and classical optimization are combined.

- [Section index](05-variational-quantum-algorithms/README.md)
- [PQC and Ansatz](05-variational-quantum-algorithms/01-pqc-and-ansatz.md)
- [Variational Principle and Hybrid Loop](05-variational-quantum-algorithms/02-variational-principle.md)
- [VQE](05-variational-quantum-algorithms/03-vqe.md)
- [QAOA](05-variational-quantum-algorithms/04-qaoa.md)
- [Optimization and Gradients](05-variational-quantum-algorithms/05-optimization-and-gradients.md)
- [Barren Plateaus and Trainability](05-variational-quantum-algorithms/06-barren-plateaus.md)

## 6. Quantum Information Theory

Develop the language of states, channels, entropy, communication, resources, and error correction.

- [Section index](06-quantum-information-theory/README.md)
- [Quantum Channels](06-quantum-information-theory/01-quantum-channels.md)
- [Entropy and Information](06-quantum-information-theory/02-entropy-and-information.md)
- [Entanglement Theory](06-quantum-information-theory/03-entanglement-theory.md)
- [Quantum Resource Theories](06-quantum-information-theory/04-resource-theories.md)
- [Quantum Communication](06-quantum-information-theory/05-quantum-communication.md)
- [Quantum Error Correction](06-quantum-information-theory/06-error-correction.md)

## 7. Quantum Machine Learning

Learn the main QML paradigms and the distinctions among data encoding, trainable circuits, kernels, structured models, learning from quantum data, trainability, generalization, and quantum advantage.

- [Section index](07-quantum-machine-learning/README.md)
- [What Is QML?](07-quantum-machine-learning/01-what-is-qml.md)
- [Data Access and Quantum Encoding](07-quantum-machine-learning/02-data-encoding.md)
- [PQC, VQC, and QNN Terminology](07-quantum-machine-learning/03-pqc-vqc-qnn.md)
- [Quantum Kernel Methods](07-quantum-machine-learning/04-quantum-kernels.md)
- [QCNNs and Structured Architectures](07-quantum-machine-learning/05-qcnn.md)
- [Quantum Generative Models](07-quantum-machine-learning/06-generative-qml.md)
- [Quantum Reservoir Computing](07-quantum-machine-learning/07-quantum-reservoir-computing.md)
- [Quantum Reinforcement Learning](07-quantum-machine-learning/08-quantum-reinforcement-learning.md)
- [Quantum Learning Theory](07-quantum-machine-learning/09-quantum-learning-theory.md)
- [Learning from Quantum Data](07-quantum-machine-learning/10-learning-from-quantum-data.md)
- [Generalization](07-quantum-machine-learning/11-generalization.md)
- [Trainability](07-quantum-machine-learning/12-trainability.md)
- [Quantum Advantage in Learning](07-quantum-machine-learning/13-quantum-advantage.md)

## 8. Reference

Use these files when a symbol or acronym becomes unclear.

- [Reference index](08-reference/README.md)
- [Notation](08-reference/notation.md)
- [Terminology Map](08-reference/terminology-map.md)
- [Glossary](08-reference/glossary.md)
- [Bibliography](08-reference/bibliography.md)

## A terminology rule used throughout the book

The repository keeps the following levels separate:

```math
\boxed{
\text{physical platform}
\neq
\text{computational model}
\neq
\text{circuit object}
\neq
\text{optimization paradigm}
\neq
\text{task}
}
```

In particular:

- a **PQC** is a parameterized circuit;
- an **ansatz** is a candidate family;
- a **VQA** is a hybrid optimization framework;
- **VQE** and **QAOA** are specific VQAs;
- **QML** is a broad field;
- a **QNN** is architecture-dependent terminology, not one uniquely defined mathematical object.

See the [Terminology Map](08-reference/terminology-map.md) for a compact summary.

## Educational principles

The text follows a few simple rules:

1. Introduce intuition before using heavy notation where possible.
2. State assumptions explicitly.
3. Distinguish mathematical models from physical hardware.
4. Explain what an equation means, not only how to manipulate it.
5. Include worked examples and exercises where they add value.
6. Distinguish established results from common heuristics or oversimplifications.
7. Treat quantum advantage carefully, while keeping the presentation accessible to learners.

Primary papers, major reviews, textbooks, and formal standards are prioritized in the references. General quantum-computing vocabulary is aligned where possible with [ISO/IEC 4879:2024](https://www.iso.org/standard/80432.html).

## Status

The repository now contains a complete first educational pass covering quantum-information foundations, computational models, hardware, algorithms, variational methods, quantum information theory, and quantum machine learning. Future revisions should primarily improve pedagogy: clearer examples, additional exercises and solutions, diagrams, cross-links, and explanations of common points of confusion.
