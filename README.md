# Quantum Computing: From Quantum Information to Quantum Machine Learning

A structured, research-oriented introduction to **quantum information science (QIS)**, **quantum computing**, and **quantum machine learning (QML)**.

The goal of this repository is not only to introduce the standard concepts, but also to make the relationships between them explicit: computational models, physical hardware, algorithms, information-theoretic primitives, and learning paradigms are treated as distinct layers of the field.

> **Format:** the scientific content of this repository is written in Markdown (`.md`) files.

## Roadmap

### 1. Foundations

- [Quantum Information Science: The Big Picture](01-foundations/01-quantum-information-science.md)
- Classical and quantum information
- Qubits and Hilbert spaces
- Bloch-sphere representation
- Composite quantum systems and tensor products
- Entanglement
- Density operators and mixed states
- Quantum measurements and POVMs

### 2. Quantum Computing

- Gate-based / circuit model
- Adiabatic quantum computing
- Quantum annealing
- Analog quantum computing and simulation
- Measurement-based quantum computing
- Continuous-variable quantum computing

### 3. Hardware Platforms

- Superconducting qubits
- Trapped ions
- Neutral atoms
- Photonic systems
- Semiconductor and spin qubits
- Topological approaches

### 4. Quantum Algorithms

- Deutsch and Deutsch–Jozsa algorithms
- Grover search and amplitude amplification
- Quantum phase estimation
- Shor's algorithm
- Hamiltonian and quantum simulation
- Amplitude estimation

### 5. Variational Quantum Algorithms

- Parameterized quantum circuits and ansätze
- Variational principle
- Variational Quantum Eigensolver (VQE)
- Quantum Approximate Optimization Algorithm (QAOA)
- Optimization and quantum gradients
- Trainability and barren plateaus

### 6. Quantum Information Theory

- Quantum states and density operators
- Quantum measurements
- Quantum channels and open systems
- Quantum entropy and information measures
- Entanglement theory
- Quantum communication
- Resource theories
- Quantum error correction

### 7. Quantum Machine Learning

- What is quantum machine learning?
- Classical data versus quantum data
- Quantum data encoding
- PQCs, variational quantum models, VQCs, and QNNs
- Quantum kernel methods
- Quantum convolutional neural networks and structured architectures
- Quantum generative models
- Quantum reservoir computing
- Quantum reinforcement learning
- Learning quantum states, channels, Hamiltonians, and processes
- Trainability and optimization
- Generalization
- Quantum learning advantage

### 8. Reference

- [Notation](08-reference/notation.md)
- [Terminology Map](08-reference/terminology-map.md)
- Glossary
- Bibliography

## Conceptual Map

```text
QUANTUM INFORMATION SCIENCE
│
├── Quantum Computing
│   │
│   ├── Computational Models
│   │   ├── Gate-Based / Circuit Model
│   │   ├── Adiabatic Quantum Computing
│   │   ├── Quantum Annealing
│   │   ├── Analog Quantum Computing / Simulation
│   │   ├── Measurement-Based Quantum Computing
│   │   └── Continuous-Variable Quantum Computing
│   │
│   ├── Physical Hardware Platforms
│   │   ├── Superconducting Qubits
│   │   ├── Trapped Ions
│   │   ├── Neutral Atoms
│   │   ├── Photonic Systems
│   │   ├── Semiconductor / Spin Qubits
│   │   └── Topological Approaches
│   │
│   ├── Quantum Algorithms
│   │   ├── Shor's Algorithm
│   │   ├── Grover's Algorithm
│   │   ├── Quantum Simulation
│   │   ├── Quantum Phase Estimation
│   │   ├── Amplitude Amplification / Estimation
│   │   └── Variational Quantum Algorithms
│   │       ├── VQE
│   │       ├── QAOA
│   │       └── Other VQAs
│   │
│   └── Fault-Tolerant Quantum Computing
│       ├── Physical Qubits
│       ├── Quantum Error Correction
│       ├── Logical Qubits
│       └── Fault-Tolerant Logical Operations
│
├── Quantum Information Theory
│   ├── Quantum States and Density Operators
│   ├── Composite Systems and Entanglement
│   ├── Quantum Measurements and POVMs
│   ├── Quantum Channels and Open Systems
│   ├── Quantum Entropy and Information Measures
│   ├── Quantum Communication
│   ├── Quantum Resource Theories
│   └── Quantum Error Correction
│
└── Quantum Machine Learning
    │
    ├── Variational Quantum Machine Learning
    │   ├── Parameterized Quantum Circuits (PQCs)
    │   ├── Variational Quantum Models / Classifiers
    │   ├── Quantum Neural Networks (QNNs)
    │   └── Structured Architectures
    │
    ├── Quantum Kernel Methods
    ├── Quantum Generative Models
    ├── Quantum Reservoir Computing
    ├── Quantum Reinforcement Learning
    ├── Quantum Learning Theory
    │
    └── Learning from Quantum Data
        ├── Quantum-State Learning
        ├── Quantum-Channel Learning
        ├── Hamiltonian Learning
        └── Quantum-Process Learning
```

## Terminology Principle

Throughout the repository, we distinguish four levels that are frequently conflated in the literature:

1. **Computational object** — for example, a parameterized quantum circuit \(U(\boldsymbol{\theta})\).
2. **Representation or hypothesis family** — for example, an ansatz.
3. **Optimization or learning paradigm** — for example, a variational quantum algorithm.
4. **Task or application** — for example, classification, ground-state estimation, or combinatorial optimization.

This distinction will be used consistently when discussing terms such as **PQC**, **VQC**, **QNN**, **VQA**, **VQE**, and **QAOA**.

## Scope

The repository aims to develop enough mathematical and physical background to read modern papers in quantum algorithms and QML critically, including their assumptions about data access, resources, trainability, classical simulability, and quantum advantage.
