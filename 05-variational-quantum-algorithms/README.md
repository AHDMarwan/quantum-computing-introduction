# Variational Quantum Algorithms

Variational quantum algorithms (VQAs) combine parameterized quantum computations with classical optimization. They form an algorithmic paradigm, not a single algorithm and not a synonym for quantum machine learning.

## Contents

1. [Parameterized Quantum Circuits and Ansätze](01-pqc-and-ansatz.md)
2. [Variational Principle and Hybrid Loop](02-variational-principle.md)
3. [Variational Quantum Eigensolver](03-vqe.md)
4. [Quantum Approximate Optimization Algorithm](04-qaoa.md)
5. [Optimization, Gradients, and Measurement Cost](05-optimization-and-gradients.md)
6. [Barren Plateaus and Trainability](06-barren-plateaus.md)

## Terminology hierarchy

```math
\boxed{
\text{PQC: parameterized circuit}
\neq
\text{VQA: optimization framework}
}
```

An ansatz specifies a family of candidate states or transformations. A PQC can implement an ansatz. A VQA uses a parameterized quantum object, a cost estimator, and a classical update rule. VQE and QAOA are specific VQAs.

See also [Terminology Map](../08-reference/terminology-map.md).
