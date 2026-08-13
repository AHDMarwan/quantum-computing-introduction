# Quantum Algorithms

This section develops canonical quantum algorithms as **resource-aware computational procedures**, not as collections of circuit diagrams.

The central objective is to understand exactly where a quantum improvement comes from and what assumptions are required for the complexity claim to be meaningful.

## Recommended learning path

```text
promise problems and oracle interference
-> amplitude amplification
-> spectral phase extraction
-> number-theoretic period finding
-> Hamiltonian simulation
-> numerical amplitude estimation
```

This sequence is deliberate. Later chapters reuse primitives introduced earlier.

## Contents

1. [Deutsch–Jozsa Algorithm](01-deutsch-jozsa.md)
2. [Grover Search and Amplitude Amplification](02-grover.md)
3. [Quantum Phase Estimation](03-phase-estimation.md)
4. [Shor's Algorithm](04-shor.md)
5. [Quantum Simulation](05-quantum-simulation.md)
6. [Quantum Amplitude Estimation](06-amplitude-estimation.md)

## Phase 3 chapter standard

Every algorithm chapter is organized around the following questions:

```text
problem definition
-> input / oracle / access model
-> classical baseline
-> quantum primitive
-> derivation
-> correctness
-> asymptotic complexity
-> physical resource accounting
-> source of quantum improvement
-> limitations and hidden assumptions
-> exercises
```

The purpose of this structure is to prevent a common mistake in quantum computing: quoting an asymptotic quantum complexity without specifying the computational model in which it was obtained.

## The resource-accounting principle

A quantum algorithm can have several different notions of cost:

- **query complexity** — number of oracle calls,
- **gate complexity** — number of elementary quantum gates,
- **circuit depth** — longest dependency chain of gates,
- **qubit complexity** — logical or physical qubits required,
- **coherent evolution time** — how long quantum information must remain coherent,
- **measurement complexity** — number of shots or observables,
- **state-preparation complexity** — cost of preparing input states,
- **data-access complexity** — cost of loading or accessing classical information coherently,
- **fault-tolerant overhead** — resources needed to realize reliable logical operations.

Therefore

```math
\text{quantum query advantage}
\not\Rightarrow
\text{end-to-end runtime advantage}.
```

A full comparison must identify the resource being improved.

## A recurring audit checklist

For every quantum algorithm, ask:

1. **What is the precise computational problem?**
2. **What promise, if any, is assumed?**
3. **How is the input represented?**
4. **How is the input accessed coherently?**
5. **What is the strongest relevant classical baseline?**
6. **What quantum primitive creates the improvement?**
7. **What complexity measure is being quoted?**
8. **What costs are hidden inside an oracle or state-preparation primitive?**
9. **What output is actually required?**
10. **How many measurements are needed?**
11. **How does precision affect the cost?**
12. **What changes in a fault-tolerant implementation?**

## Learning goals

After completing this section, you should be able to:

- distinguish deterministic, randomized, and quantum query complexity,
- derive phase kickback in oracle algorithms,
- explain Deutsch–Jozsa as a global interference computation,
- derive Grover search as a two-dimensional rotation,
- explain why Grover's quadratic query speedup is optimal for black-box unstructured search,
- generalize Grover search to amplitude amplification,
- derive the Fourier phase state used by quantum phase estimation,
- connect QPE precision to controlled evolution time,
- explain how Shor reduces factoring to order finding,
- distinguish Shor's complexity-theoretic result from practical fault-tolerant resource requirements,
- derive first-order Hamiltonian product formulas,
- explain how noncommutativity controls Trotter error,
- distinguish digital and analog quantum simulation,
- analyze the output and measurement problem in quantum simulation,
- derive the relation between amplitude estimation and Grover eigenphases,
- compare $O(1/\epsilon^2)$ Monte Carlo sampling with ideal $O(1/\epsilon)$ coherent amplitude estimation,
- and audit quantum-advantage claims using end-to-end resource accounting.

## Algorithm comparison map

| Algorithm | Core task | Main primitive | Typical headline advantage |
|---|---|---|---|
| Deutsch–Jozsa | Promise-property testing | Phase kickback + interference | Exact deterministic query separation |
| Grover | Unstructured search | Amplitude amplification | Quadratic query improvement |
| QPE | Eigenphase estimation | Controlled powers + inverse QFT | Spectral information extraction |
| Shor | Factoring / discrete log | Order finding + QPE/QFT | Polynomial-time quantum algorithm |
| Quantum simulation | Approximate quantum dynamics | Product formulas / block encodings / signal processing | Efficient structured quantum evolution |
| Amplitude estimation | Probability / expectation estimation | Grover eigenphase estimation | Quadratic precision-query improvement |

The table gives only the headline. Each chapter explains the access model and caveats required to interpret that statement correctly.

## Three recurring mechanisms

Although the algorithms look different, several patterns repeat.

### 1. Phase encoding

Information is converted into relative phase:

```text
function value / eigenvalue
-> phase
```

This appears in Deutsch–Jozsa, QPE, Shor, and amplitude estimation.

### 2. Interference or spectral decoding

A unitary transformation makes the encoded phase observable:

```text
phase structure
-> interference / Fourier transform
-> measurable classical information
```

### 3. Structured access

The algorithm assumes the relevant operation can be applied coherently:

```text
oracle
controlled unitary
Hamiltonian evolution
state-preparation circuit
```

These are computational resources, not free abstractions.

## Suggested study method

For each chapter:

1. Write down the problem before reading the circuit.
2. Identify the classical baseline.
3. Write the quantum state after every conceptually important operation.
4. Derive the final measurement probability rather than memorizing it.
5. State the asymptotic complexity and name the resource it counts.
6. List any oracle, QRAM, state-preparation, precision, or fault-tolerance assumptions.
7. Complete at least one computational exercise.
8. Answer the research-oriented exercises as if reviewing a paper's quantum-advantage claim.

## Why this matters for QML

Quantum machine learning inherits the same methodological problems as quantum algorithms, often in a harder form.

A QML pipeline may contain

```text
classical data
-> quantum encoding
-> trainable quantum circuit
-> measurements
-> classical optimization.
```

If only the circuit evaluation is counted while encoding, sampling, training, or classical baselines are ignored, a claimed advantage can be misleading.

The habits developed in this section therefore become the foundation for later analysis of QML:

```math
\boxed{
\text{task}
+
\text{access model}
+
\text{resource metric}
+
\text{classical baseline}
}
```

must be specified before the phrase **quantum advantage** becomes operationally meaningful.

## Core references

- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
- J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
- L. K. Grover, "A fast quantum mechanical algorithm for database search," STOC (1996).
- P. W. Shor, "Algorithms for quantum computation: discrete logarithms and factoring," FOCS (1994).
- S. Lloyd, "Universal Quantum Simulators," *Science* 273, 1073–1078 (1996).
- G. Brassard, P. Høyer, M. Mosca, and A. Tapp, "Quantum Amplitude Amplification and Estimation." https://arxiv.org/abs/quant-ph/0005055
