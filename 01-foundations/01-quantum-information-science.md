# Quantum Information Science: The Big Picture

## 1. Motivation

Quantum information science (QIS) studies how information is represented, processed, transmitted, learned, and protected when the underlying physical systems obey quantum mechanics.

The field lies at the intersection of quantum physics, computer science, mathematics, information theory, and engineering. Its central shift in viewpoint is to treat quantum states, transformations, measurements, and correlations not only as physical phenomena, but also as **information-processing resources**.

This chapter provides a map of the field before introducing the mathematical foundations in detail.

> **Important:** the taxonomy below is pedagogical rather than a strict partition. Quantum computing, quantum information theory, quantum communication, error correction, and quantum machine learning overlap substantially.

## 2. Classical and Quantum Information

A classical bit takes a value in

\[
\{0,1\}.
\]

A qubit is described, in the pure-state formalism, by a normalized vector in a two-dimensional complex Hilbert space:

\[
|\psi\rangle
=
\alpha|0\rangle+
\beta|1\rangle,
\qquad
|\alpha|^2+|\beta|^2=1.
\]

The coefficients \(\alpha\) and \(\beta\) are complex probability amplitudes. They are not ordinary probabilities. Probabilities arise when a measurement is performed.

For example, a measurement in the computational basis gives

\[
p(0)=|\alpha|^2,
\qquad
p(1)=|\beta|^2.
\]

For \(n\) qubits, the state space is

\[
\mathcal H=(\mathbb C^2)^{\otimes n},
\]

with dimension

\[
\dim(\mathcal H)=2^n.
\]

The exponential dimension of this Hilbert space is fundamental, but it should not be confused with an automatic exponential computational advantage. Measurement does not reveal all amplitudes of a quantum state, and useful quantum algorithms must organize the dynamics and interference so that relevant global information becomes observable with controlled resources.

## 3. Core Quantum-Information Primitives

Several recurring concepts appear throughout QIS.

### 3.1 Superposition

A quantum state may contain coherent amplitudes associated with multiple basis states:

\[
|\psi\rangle
=
\sum_x \alpha_x |x\rangle.
\]

Superposition is meaningful because the relative phases of the amplitudes can affect subsequent operations and measurements.

### 3.2 Interference

Quantum amplitudes can combine constructively or destructively. Quantum algorithms exploit interference to amplify useful components and suppress others.

### 3.3 Entanglement

A composite state is entangled when it cannot be written as a product of states of its subsystems. For example,

\[
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
\]

cannot be expressed as

\[
|\psi_A\rangle\otimes|\psi_B\rangle.
\]

Entanglement is a central resource in quantum communication, computation, sensing, and information theory, but its presence alone does not establish a computational advantage.

### 3.4 Measurement

Quantum measurements convert quantum information into classical outcomes. General measurements are described by positive-operator-valued measures (POVMs), which will be introduced later.

### 3.5 Quantum Dynamics

Closed-system dynamics are represented by unitary transformations,

\[
\rho\mapsto U\rho U^\dagger,
\]

while general physical transformations, including noise and interaction with an environment, are represented by quantum channels,

\[
\rho\mapsto\mathcal E(\rho).
\]

These objects form the common mathematical language underlying quantum computing and quantum information theory.

## 4. A Map of Quantum Information Science

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

The purpose of this map is to distinguish several levels of description that are frequently mixed together.

## 5. Computational Models Are Not Hardware Platforms

A **computational model** specifies how a computation is represented mathematically.

A **hardware platform** specifies the physical degrees of freedom used to realize quantum information processing.

A **quantum algorithm** specifies a procedure for solving a problem within a computational model.

These are different levels.

For example, a gate-based quantum algorithm is not intrinsically a superconducting algorithm. Gate-based computation can be implemented using superconducting qubits, trapped ions, neutral atoms, photonic systems, or other suitable technologies.

## 6. Main Computational Models

### 6.1 Gate-Based / Circuit Quantum Computing

The circuit model represents a computation as a sequence of quantum operations. For a closed-system unitary computation,

\[
|\psi_{\mathrm{out}}\rangle
=
U_L U_{L-1}\cdots U_1
|\psi_{\mathrm{in}}\rangle.
\]

Measurements are then performed to extract classical outcomes.

This is the dominant language for general-purpose quantum algorithms and for most current work on parameterized quantum circuits and variational quantum machine learning.

### 6.2 Adiabatic Quantum Computing

Adiabatic quantum computation uses controlled Hamiltonian evolution. A common interpolation is

\[
H(s)=(1-s)H_0+sH_P,
\qquad 0\le s\le1,
\]

where \(H_0\) has an easily prepared ground state and \(H_P\) encodes the target problem.

Under appropriate conditions, sufficiently slow evolution keeps the state close to the instantaneous ground state. The standard adiabatic model is polynomially equivalent to the circuit model.

### 6.3 Quantum Annealing

Quantum annealing is closely related to adiabatic evolution but is generally used as an optimization paradigm. Problems are often encoded into Ising or QUBO energy functions, and the physical evolution is designed to find low-energy configurations.

Quantum annealing and universal adiabatic quantum computing should therefore not be treated as exact synonyms.

### 6.4 Analog Quantum Simulation

In analog quantum simulation, one engineers a controllable quantum system whose Hamiltonian directly reproduces or approximates the target dynamics:

\[
|\psi(t)\rangle=e^{-iHt}|\psi(0)\rangle.
\]

Rather than decomposing the full evolution into elementary digital gates, the physical dynamics themselves implement the computation or simulation.

### 6.5 Measurement-Based Quantum Computing

Measurement-based quantum computing begins with an entangled resource state, such as a cluster state. Computation is then driven by a sequence of local measurements whose bases can depend on previous outcomes.

This demonstrates that universal quantum computation does not require the circuit model as its fundamental operational description.

### 6.6 Continuous-Variable Quantum Computing

Continuous-variable quantum computing encodes and manipulates information using quantum systems with continuous observables, such as optical field quadratures. It is particularly relevant to photonic quantum computing.

## 7. Hardware Platforms

Quantum information can be encoded in many different physical systems, including

- superconducting circuits,
- trapped ions,
- neutral atoms,
- photons and optical modes,
- electronic or nuclear spins,
- and proposed topological encodings.

Different platforms exhibit different trade-offs in coherence, gate fidelity, connectivity, measurement, control, fabrication, operating conditions, and scalability.

No single hardware platform should therefore be identified with quantum computing itself.

## 8. Quantum Algorithms

Quantum algorithms exploit quantum information-processing primitives to solve computational problems.

Important algorithmic families include

- factoring and hidden-subgroup algorithms,
- quantum search and amplitude amplification,
- phase estimation,
- Hamiltonian and quantum simulation,
- amplitude estimation,
- and hybrid variational algorithms.

Two canonical examples are Shor's factoring algorithm and Grover's unstructured-search algorithm. Other algorithms, such as quantum phase estimation, serve as primitives inside larger quantum algorithms.

## 9. Variational Quantum Algorithms

A variational quantum algorithm (VQA) uses a parameterized quantum computation together with a classical optimization loop.

A generic structure is

\[
\boldsymbol\theta_t
\rightarrow
U(\boldsymbol\theta_t)
\rightarrow
C(\boldsymbol\theta_t)
\rightarrow
\text{classical optimizer}
\rightarrow
\boldsymbol\theta_{t+1}.
\]

The Variational Quantum Eigensolver (VQE) and Quantum Approximate Optimization Algorithm (QAOA) are prominent examples.

A parameterized quantum circuit is a component that may be used inside such an algorithm; it is not synonymous with the full variational algorithm.

See [Terminology Map](../08-reference/terminology-map.md).

## 10. Quantum Information Theory

Quantum information theory develops the mathematical principles governing quantum information.

Core subjects include

- density operators,
- quantum measurements,
- quantum channels,
- entanglement,
- entropy and information measures,
- channel capacities,
- quantum communication,
- resource theories,
- and quantum error correction.

This theory provides much of the language required to analyze quantum algorithms and quantum learning models rigorously.

## 11. Quantum Machine Learning

Quantum machine learning (QML) investigates learning problems in which quantum information processing, quantum models, or quantum data play a nontrivial role.

QML is not a single algorithm and is not synonymous with parameterized quantum circuits.

Important directions include

- variational quantum learning,
- quantum kernels,
- quantum generative models,
- quantum reservoir computing,
- quantum reinforcement learning,
- quantum learning theory,
- and learning directly from quantum data.

A particularly important distinction is between **classical data encoded into a quantum system** and **data that are quantum from the beginning**.

For classical data,

\[
x\in\mathcal X
\quad\longmapsto\quad
\rho(x),
\]

so the data-access and encoding model becomes part of the computational cost.

For quantum data, the learner may instead receive quantum states, channels, Hamiltonian-generated dynamics, or more general quantum processes directly.

## 12. Fault Tolerance and Quantum Error Correction

Real quantum systems are noisy. General noisy dynamics are described by quantum channels rather than ideal unitary transformations.

Quantum error correction encodes logical quantum information into larger physical systems so that errors can be detected and corrected without directly measuring the protected logical information.

The long-term goal of fault-tolerant quantum computing is to perform arbitrarily long computations with controlled logical error rates, provided physical noise satisfies appropriate conditions and sufficient error-correction resources are available.

This distinction between physical and logical qubits becomes essential when discussing the practical resources required by quantum algorithms.

## 13. What This Repository Will Emphasize

The repository will distinguish carefully between

\[
\text{physical system},
\quad
\text{mathematical model},
\quad
\text{algorithm},
\quad
\text{learning model},
\quad
\text{resource assumption}.
\]

When discussing claims of quantum advantage, we will ask what resource is being counted, what input-access model is assumed, what classical competitor is used, and whether the advantage concerns runtime, queries, samples, representation, or another operational quantity.

## 14. Next Steps

The next foundations chapters will introduce

1. classical versus quantum information,
2. Hilbert spaces and bra-ket notation,
3. qubits and the Bloch sphere,
4. tensor products and composite systems,
5. entanglement,
6. density operators,
7. measurements and POVMs,
8. and quantum channels.

These concepts will then be used to build the circuit model, quantum algorithms, variational algorithms, and quantum machine learning.

## References

1. John Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
2. John Preskill, *Quantum Computation Lecture Notes*, California Institute of Technology. https://www.preskill.caltech.edu/ph229/
3. ISO/IEC 4879:2024, *Information technology — Quantum computing — Vocabulary*. https://www.iso.org/standard/80432.html
4. D. Aharonov, W. van Dam, J. Kempe, Z. Landau, S. Lloyd, O. Regev, *Adiabatic Quantum Computation is Equivalent to Standard Quantum Computation*. https://arxiv.org/abs/quant-ph/0405098
5. R. Raussendorf and H. J. Briegel, *A One-Way Quantum Computer*. https://arxiv.org/abs/quant-ph/0108118
6. S. Lloyd and S. L. Braunstein, *Quantum Computation over Continuous Variables*. https://arxiv.org/abs/quant-ph/9810082
