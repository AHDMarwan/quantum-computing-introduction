# Foundations

This section develops the mathematical language used throughout the repository. The order is deliberate: we first distinguish classical probabilities from quantum amplitudes, then introduce Hilbert spaces and single-qubit geometry, then composite systems, entanglement, mixed states, and finally measurement.

The goal is not only to recognize definitions. By the end of the section, you should be able to **derive, calculate, compare, and explain** the main objects of elementary quantum information.

## Recommended learning path

```text
classical probability
→ quantum amplitudes and phase
→ Hilbert-space formalism
→ single-qubit geometry
→ tensor-product composition
→ entanglement
→ density operators
→ measurement and POVMs
```

Each step introduces ideas needed by the next one.

## Contents

1. [Quantum Information Science: The Big Picture](01-quantum-information-science.md)
2. [Classical vs Quantum Information](02-classical-vs-quantum-information.md)
3. [Qubits and Hilbert Spaces](03-qubits-and-hilbert-spaces.md)
4. [The Bloch Sphere](04-bloch-sphere.md)
5. [Composite Systems and Tensor Products](05-composite-systems.md)
6. [Entanglement](06-entanglement.md)
7. [Density Matrices and Mixed States](07-density-matrices.md)
8. [Measurements and POVMs](08-measurements-and-povms.md)

## How the chapters are written

The core foundations chapters are designed as lecture notes rather than short encyclopedia entries. Where appropriate they include:

```text
motivation
→ learning objectives
→ formal definitions
→ derivations
→ worked examples
→ common misconceptions
→ connections to later topics
→ conceptual exercises
→ computational exercises
→ challenge exercises
→ key takeaways
```

The challenge exercises are optional. They are meant to connect several ideas at once and test understanding beyond direct substitution into formulas.

## Learning goals

After completing this section, you should be able to:

- distinguish classical probabilities from complex quantum amplitudes,
- explain global phase, relative phase, and interference,
- manipulate bras, kets, inner products, outer products, and operators,
- distinguish unitary, Hermitian, positive, and projective operators,
- expand one-qubit operators in the Pauli basis,
- derive the two-parameter representation of a pure qubit,
- convert between qubit states, density matrices, and Bloch vectors,
- interpret Pauli measurements geometrically,
- construct multipartite state spaces using tensor products,
- distinguish product states from entangled states,
- compute reduced density operators using partial traces,
- use Schmidt decomposition for bipartite pure states,
- distinguish entanglement from classical correlation and Bell nonlocality,
- use density operators for mixed states, subsystems, and noisy evolution,
- compute purity, expectation values, and basic distinguishability measures,
- distinguish projective measurements, POVMs, and quantum instruments,
- analyze finite-shot expectation-value estimation,
- and formulate basic state-discrimination problems.

## Suggested study method

For each chapter:

1. Read the conceptual sections first without trying to memorize formulas.
2. Reproduce the main derivations by hand.
3. Work through the examples without looking at the intermediate steps.
4. Answer the conceptual exercises in prose.
5. Solve the computational exercises explicitly.
6. Try the challenge exercises only after the main ideas feel comfortable.

A useful checkpoint is that you should be able to move freely between

```text
state vector
↔ density matrix
↔ observable statistics
↔ geometric or subsystem interpretation
```

without treating these representations as interchangeable objects.

## What comes next

Once these foundations are comfortable, continue to:

- [Computational Models of Quantum Computing](../02-quantum-computing/README.md),
- then [Quantum Algorithms](../04-quantum-algorithms/README.md),
- then [Variational Quantum Algorithms](../05-variational-quantum-algorithms/README.md),
- and later [Quantum Machine Learning](../07-quantum-machine-learning/README.md).

The later chapters assume the notation and distinctions established here.

## Core references

- J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
- J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
