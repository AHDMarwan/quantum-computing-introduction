# Notation

This file defines the default mathematical notation used throughout the repository. Individual chapters may introduce additional symbols, but they should not redefine the symbols listed here without an explicit warning.

## Linear Algebra and Quantum States

| Symbol | Meaning |
|---|---|
| $\mathcal H$ | Hilbert space |
| $\mathcal H_A \otimes \mathcal H_B$ | Composite Hilbert space of systems $A$ and $B$ |
| $|\psi\rangle$ | Pure quantum state vector |
| $\langle\psi|$ | Dual vector (bra) associated with $|\psi\rangle$ |
| $\langle\phi|\psi\rangle$ | Inner product |
| $|\phi\rangle\langle\psi|$ | Outer product |
| $\rho$ | Density operator / density matrix |
| $I$ | Identity operator |
| $A^\dagger$ | Adjoint (conjugate transpose) of operator $A$ |
| $\mathrm{Tr}(A)$ | Trace of $A$ |
| $\mathrm{Tr}_B(\rho_{AB})$ | Partial trace over subsystem $B$ |

## Quantum Dynamics

| Symbol | Meaning |
|---|---|
| $U$ | Unitary operator |
| $U(\boldsymbol\theta)$ | Parameterized unitary / quantum circuit |
| $H$ | Hamiltonian |
| $e^{-iHt}$ | Unitary time-evolution operator (with $\hbar=1$) |
| $\mathcal E$ | Quantum channel / completely positive trace-preserving map |
| $K_j$ | Kraus operator |

## Measurements

| Symbol | Meaning |
|---|---|
| $M$ | Observable or measurement operator, depending on context |
| $\{E_y\}_y$ | POVM with outcome labels $y$ |
| $p(y)$ | Probability of outcome $y$ |
| $\langle M\rangle_\rho$ | Expectation value $\mathrm{Tr}(\rho M)$ |

## Quantum Computing

| Symbol | Meaning |
|---|---|
| $n$ | Number of qubits, unless specified otherwise |
| $|0\rangle^{\otimes n}$ | $n$-qubit all-zero state |
| $L$ | Circuit depth or number of layers, depending on context |
| $p$ | QAOA depth parameter when discussing QAOA |

## Optimization and Quantum Machine Learning

| Symbol | Meaning |
|---|---|
| $x$ | Classical input / data point |
| $y$ | Label, target, or measurement outcome depending on context |
| $\boldsymbol\theta$ | Trainable model parameters |
| $U_\phi(x)$ | Data-encoding unitary / quantum feature map |
| $U(\boldsymbol\theta)$ | Trainable parameterized quantum circuit |
| $f_{\boldsymbol\theta}(x)$ | Model prediction |
| $\mathcal L(\boldsymbol\theta)$ | Loss function |
| $C(\boldsymbol\theta)$ | Cost / objective function |
| $\Theta$ | Parameter space |
| $\mathcal F$ | Hypothesis / function class |

## Conventions

- Unless explicitly restored, we use natural units with $\hbar=1$.
- Logarithm bases are stated when they matter. In quantum information, base-2 logarithms are commonly used when entropy is measured in bits.
- The symbol $\rho$ is preferred for a general quantum state because it includes both pure and mixed states.
- The symbol $|\psi\rangle$ is used when purity is assumed or when a state-vector description is specifically required.
- A parameterized quantum circuit (PQC) is treated as a computational object. Its use as an ansatz, a variational model, or part of a learning algorithm is stated separately.

## Core References

1. John Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
2. John Preskill, *Quantum Computation Lecture Notes*, California Institute of Technology. https://www.preskill.caltech.edu/ph229/
3. ISO/IEC 4879:2024, *Information technology — Quantum computing — Vocabulary*. https://www.iso.org/standard/80432.html
