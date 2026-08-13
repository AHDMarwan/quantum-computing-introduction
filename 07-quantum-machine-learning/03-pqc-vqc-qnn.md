# PQC, VQC, and QNN Terminology

## 1. Why terminology is confusing

The QML literature frequently uses overlapping labels for related objects. The safest approach is to distinguish **object**, **training paradigm**, and **task**.

## 2. Parameterized Quantum Circuit (PQC)

A PQC is simply a circuit depending on parameters:

$$
U(\boldsymbol\theta).
$$

It can be used in chemistry, optimization, control, simulation, or machine learning. A PQC is not inherently a classifier or neural network.

## 3. Ansatz

An ansatz is the candidate family

$$
\mathcal A
=
\{U(\boldsymbol\theta)|\psi_0\rangle:\boldsymbol\theta\in\Theta\}.
$$

A PQC often implements the ansatz.

## 4. Variational quantum model

When a parameterized quantum model is optimized through an objective, it is being used variationally. A generic learning model can be written

$$
f_{\boldsymbol\theta}(x)
=
\operatorname{Tr}
\left[M\mathcal E_{\boldsymbol\theta,x}(\rho_0)\right].
$$

The map $\mathcal E$ may be unitary or a more general channel.

## 5. VQC

“VQC” is ambiguous in the literature. It may mean

- **Variational Quantum Circuit**, or
- **Variational Quantum Classifier**.

In this repository we avoid the first meaning when possible. We use **PQC** for the parameterized circuit and **variational quantum classifier (VQC)** only when the task is explicitly classification.

A binary classifier might predict

$$
\hat y=\operatorname{sign}(f_{\boldsymbol\theta}(x)).
$$

## 6. Quantum Neural Network (QNN)

“QNN” is an umbrella architectural term rather than a uniquely defined mathematical object. Many papers call trainable PQCs QNNs, while others reserve QNN for layered, convolutional, recurrent, dissipative, or network-like architectures.

Therefore a precise paper should define what it means by QNN rather than relying on the acronym.

## 7. Recommended hierarchy

This repository uses

$$
\boxed{
\text{PQC: circuit object}
}
$$

$$
\boxed{
\text{ansatz: candidate family}
}
$$

$$
\boxed{
\text{VQA: hybrid optimization framework}
}
$$

$$
\boxed{
\text{VQC: classifier using a variational quantum model}
}
$$

$$
\boxed{
\text{QNN: architecture-dependent learning terminology}
}
$$

## 8. Relation to VQE and QAOA

VQE and QAOA use parameterized circuits but are not QML algorithms by definition. VQE is an eigensolver and QAOA is an optimization algorithm. Their trainable circuits may resemble QML circuits, but the task semantics differ.

See [Terminology Map](../08-reference/terminology-map.md).

## References

1. M. Cerezo et al., "Variational quantum algorithms," *Nat. Rev. Phys.* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
2. K. Mitarai et al., "Quantum circuit learning," *Phys. Rev. A* 98, 032309 (2018). https://doi.org/10.1103/PhysRevA.98.032309
