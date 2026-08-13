# Quantum Algorithms

This section develops several canonical quantum algorithms with an emphasis on **how they work**, **why the mathematics works**, and **what kind of improvement they provide**.

The goal is not to memorize circuit diagrams. It is to understand the recurring ideas behind quantum algorithms: phase kickback, interference, amplitude amplification, Fourier structure, Hamiltonian evolution, and coherent estimation.

## Recommended learning path

```text
promise problems and oracle interference
→ amplitude amplification
→ spectral phase extraction
→ number-theoretic period finding
→ Hamiltonian simulation
→ numerical amplitude estimation
```

Later chapters reuse ideas introduced earlier.

## Contents

1. [Deutsch–Jozsa Algorithm](01-deutsch-jozsa.md)
2. [Grover Search and Amplitude Amplification](02-grover.md)
3. [Quantum Phase Estimation](03-phase-estimation.md)
4. [Shor's Algorithm](04-shor.md)
5. [Quantum Simulation](05-quantum-simulation.md)
6. [Quantum Amplitude Estimation](06-amplitude-estimation.md)

## How the chapters are organized

Each algorithm is studied through a common sequence:

```text
problem
→ input model
→ main quantum idea
→ state evolution
→ derivation
→ correctness
→ complexity
→ worked example
→ limitations / assumptions
→ exercises
```

This makes it easier to compare algorithms without reducing them to headline complexity statements.

## A note on complexity

Quantum algorithms can be analyzed using different resource measures:

- **query complexity** — number of oracle calls,
- **gate complexity** — number of elementary quantum gates,
- **circuit depth** — longest dependent sequence of gates,
- **qubit complexity** — number of qubits required,
- **coherent evolution time** — duration of controlled quantum evolution,
- **measurement complexity** — number of measurements or samples,
- **state-preparation complexity** — cost of preparing the required input state.

Therefore a statement such as “this algorithm is faster” is meaningful only after the resource being compared is identified.

For example,

```math
\text{better query complexity}
\not\Rightarrow
\text{automatically better end-to-end runtime}.
```

This distinction is introduced here because it is part of understanding the algorithms correctly.

## Learning goals

After completing this section, you should be able to:

- explain coherent oracle access and phase kickback,
- derive the interference mechanism in Deutsch–Jozsa,
- derive Grover search as a rotation in a two-dimensional subspace,
- explain amplitude amplification as the generalization of Grover search,
- describe the role of controlled powers and the inverse QFT in quantum phase estimation,
- connect QPE to energy estimation,
- explain how Shor reduces factoring to order finding,
- distinguish the number-theoretic and quantum parts of Shor's algorithm,
- derive a first-order Trotter product formula for Hamiltonian simulation,
- explain the role of noncommuting Hamiltonian terms,
- distinguish digital and analog quantum simulation,
- derive the basic idea of amplitude estimation,
- and compare the principal complexity scalings of the algorithms in this section.

## Algorithm comparison map

| Algorithm | Main task | Core idea | Main takeaway |
|---|---|---|---|
| Deutsch–Jozsa | Promise-property testing | Phase kickback + interference | A simple example of global interference |
| Grover | Unstructured search | Amplitude amplification | Quadratic query improvement |
| QPE | Eigenphase estimation | Controlled powers + inverse QFT | Extract phase/eigenvalue information |
| Shor | Factoring / discrete logarithms | Order finding + Fourier methods | Polynomial-time quantum algorithm for important number-theoretic problems |
| Quantum simulation | Quantum dynamics | Hamiltonian evolution approximations | Quantum systems can simulate structured quantum dynamics |
| Amplitude estimation | Probability / expectation estimation | Grover rotations + phase estimation | Quadratic improvement in ideal precision-query scaling |

## Three recurring ideas

### 1. Encode information in phase

```text
function value / eigenvalue
→ relative phase
```

This appears in several algorithms in different forms.

### 2. Use interference to reveal structure

```text
phase structure
→ interference or Fourier transform
→ measurement
```

The algorithm is designed so that useful information becomes likely to appear in the final measurement.

### 3. Use coherent operations

Algorithms may assume access to operations such as

```text
oracle calls
controlled unitaries
Hamiltonian evolution
state-preparation circuits
```

Understanding what these operations mean is part of understanding the algorithm.

## Suggested study method

For each chapter:

1. Write down the problem in your own words.
2. Identify the input state and the main quantum operation.
3. Follow the quantum state after each important step.
4. Derive the final measurement probability.
5. State the complexity and identify what resource it counts.
6. Work through at least one explicit example.
7. Complete the conceptual and computational exercises before moving on.

## Connection to later sections

The algorithms in this section introduce ideas that reappear later:

- QPE connects to fault-tolerant quantum simulation and chemistry.
- Hamiltonian simulation connects abstract algorithms to physical models.
- Grover and amplitude estimation introduce reusable primitives.
- Resource accounting becomes useful when studying VQAs and QML.

## Core references

- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
- J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
- L. K. Grover, "A fast quantum mechanical algorithm for database search," STOC (1996).
- P. W. Shor, "Algorithms for quantum computation: discrete logarithms and factoring," FOCS (1994).
- S. Lloyd, "Universal Quantum Simulators," *Science* 273, 1073–1078 (1996).
- G. Brassard, P. Høyer, M. Mosca, and A. Tapp, "Quantum Amplitude Amplification and Estimation." https://arxiv.org/abs/quant-ph/0005055
