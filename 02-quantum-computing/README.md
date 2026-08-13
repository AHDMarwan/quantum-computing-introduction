# Computational Models of Quantum Computing

Quantum computation can be organized through several mathematical models that describe **how information is processed**, independently from the physical hardware implementing the model.

This section separates computational model from hardware platform and algorithm.

A useful taxonomy is

```text
computational model
!=
hardware implementation
!=
algorithm.
```

For example, the gate model can be implemented using superconducting, trapped-ion, neutral-atom, or photonic hardware, while Grover's algorithm is an algorithm expressed naturally in that model.

## Recommended learning path

```text
gate / circuit model
-> adiabatic quantum computing
-> quantum annealing
-> analog quantum simulation
-> measurement-based quantum computing
-> continuous-variable quantum computing
```

## Contents

1. [Gate-Based Quantum Computing](01-gate-model.md)
2. [Adiabatic Quantum Computing](02-adiabatic-computing.md)
3. [Quantum Annealing](03-quantum-annealing.md)
4. [Analog Quantum Computing and Simulation](04-analog-quantum-computing.md)
5. [Measurement-Based Quantum Computing](05-measurement-based-qc.md)
6. [Continuous-Variable Quantum Computing](06-continuous-variable-qc.md)

## Model comparison map

| Model | Primary computational primitive | Natural resources | Typical role |
|---|---|---|---|
| Gate / circuit | discrete gates + measurements | gate count, depth, qubits, connectivity | universal digital algorithms |
| Adiabatic QC | slow Hamiltonian interpolation | evolution time, gap, locality, control | universal Hamiltonian computation |
| Quantum annealing | optimization Hamiltonian schedule | anneal time, embedding, repetitions, temperature | low-energy optimization/sampling |
| Analog simulation | native programmable dynamics | evolution time, controls, calibration, measurements | many-body simulation |
| MBQC | entangled resource + adaptive measurements | cluster size, measurement depth, feed-forward | universal measurement-driven computation |
| CV QC | bosonic modes + Gaussian/non-Gaussian operations | modes, photons, squeezing, loss | photonic/infinite-dimensional computation |

## Learning goals

After completing this section, you should be able to:

- distinguish a computational model from a physical platform,
- formulate gate-based computation in terms of unitary/channel operations and measurement,
- distinguish circuit size, depth, connectivity, and non-Clifford cost,
- explain reversible oracle embeddings and phase kickback,
- formulate adiabatic computation through time-dependent Hamiltonians,
- explain the role of the minimum spectral gap,
- distinguish universal AQC from quantum annealing,
- map QUBO problems to Ising Hamiltonians,
- analyze annealing through success probability and time to solution,
- distinguish analog simulation from digital Hamiltonian simulation,
- identify calibration and verification as analog resources,
- derive the one-bit MBQC teleportation primitive,
- explain adaptive measurement and Pauli-frame feed-forward,
- describe bosonic modes using quadratures and Fock states,
- distinguish Gaussian and non-Gaussian CV resources,
- and recognize which QML architectures naturally belong to each computational model.

## A recurring resource principle

Each model has its own natural complexity quantities.

Gate computation emphasizes

```text
gates + depth + qubits.
```

Adiabatic computation emphasizes

```text
time + spectral gap + Hamiltonian locality.
```

Analog simulation emphasizes

```text
native interaction + control precision + measurement.
```

MBQC emphasizes

```text
resource-state preparation + measurement dependency depth.
```

CV computation emphasizes

```text
modes + energy + squeezing + non-Gaussianity + loss.
```

Therefore cross-model comparisons should not reduce everything to one arbitrary metric without explaining the conversion.

## Computational equivalence versus physical efficiency

Several universal models can simulate one another with polynomial overhead.

This means they belong to the same broad complexity class under standard abstractions.

It does **not** mean they are equally efficient on real hardware.

A physical platform may implement one model's native primitives much more naturally than another's.

The distinction is

```math
\boxed{
\text{computational equivalence}
\not\Rightarrow
\text{equal physical resource cost}
}
```

## Where QML fits

Most variational QML uses the gate model:

```math
x
\xrightarrow{U_\phi(x)}
|\phi(x)\rangle
\xrightarrow{U_\theta}
|\psi(x,\theta)\rangle
\xrightarrow{M}
y.
```

But alternative QML paradigms include:

```text
analog Hamiltonian feature maps
quantum reservoir dynamics
MBQC measurement-policy learners
continuous-variable photonic models
annealing-based optimization/sampling.
```

Understanding computational models therefore prevents QML from being artificially identified with one circuit architecture.

## Suggested study method

For each model:

1. Identify the primitive operation.
2. Identify the state representation.
3. Identify where programmability enters.
4. Identify how output is measured.
5. List the natural computational resources.
6. Identify which hardware platforms support the primitive naturally.
7. Ask whether the model is universal or task specialized.
8. Connect it to one algorithm and one possible QML architecture.

## Core references

- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
- D. Aharonov et al., "Adiabatic Quantum Computation is Equivalent to Standard Quantum Computation," *SIAM Journal on Computing* 37, 166–194 (2007).
- R. Raussendorf and H. J. Briegel, "A One-Way Quantum Computer," *Physical Review Letters* 86, 5188 (2001).
- S. Lloyd and S. L. Braunstein, "Quantum Computation over Continuous Variables," *Physical Review Letters* 82, 1784 (1999).
