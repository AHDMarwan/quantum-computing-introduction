# Measurement-Based Quantum Computing

## 1. Different computational logic

Measurement-based quantum computing (MBQC) performs universal computation by first preparing a highly entangled resource state and then executing a sequence of local measurements. The computation is driven by the measurement choices and classical feed-forward rather than by a conventional sequence of unitary gates.

The canonical resource is a cluster or graph state.

## 2. Graph-state resource

Given a graph \(G=(V,E)\), a graph state can be prepared by placing each vertex in \(|+\rangle\) and applying controlled-\(Z\) gates along edges:

\[
|G\rangle
=
\prod_{(i,j)\in E}CZ_{ij}|+\rangle^{\otimes |V|}.
\]

The state is prepared before most of the logical computation is known operationally.

## 3. Computation by measurement

Single-qubit measurements are performed in selected bases. Measurement outcomes are random, but their effect can be tracked through byproduct operators. Later measurement bases can depend on earlier outcomes.

This adaptive classical feed-forward is essential for deterministic logical behavior.

## 4. One-way character

After a qubit is measured, it is consumed as part of the resource. The entanglement structure is progressively destroyed while logical information propagates through the resource state. This motivates the name “one-way quantum computer.”

## 5. Universality

Raussendorf and Briegel showed that suitable cluster states with adaptive single-qubit measurements support universal quantum computation. MBQC is therefore not merely a special-purpose protocol.

## 6. Why MBQC matters conceptually

MBQC shows that

\[
\text{quantum computation}\neq\text{unitary gate sequence only}.
\]

It separates **resource-state preparation** from **computation by measurement**. This perspective is especially relevant when thinking about measurement-driven QML, photonic architectures, and resource theories of computation.

## References

1. R. Raussendorf and H. J. Briegel, "A One-Way Quantum Computer," *Phys. Rev. Lett.* 86, 5188 (2001). https://doi.org/10.1103/PhysRevLett.86.5188
2. R. Raussendorf, D. E. Browne, and H. J. Briegel, "Measurement-based quantum computation on cluster states," *Phys. Rev. A* 68, 022312 (2003). https://doi.org/10.1103/PhysRevA.68.022312
