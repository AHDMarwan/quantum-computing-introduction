# Data Access and Quantum Encoding

## 1. Encoding is part of the algorithm

When input data are classical, a quantum learner must specify how they enter the quantum system. A feature map is a transformation

\[
x\longmapsto \rho(x)
\]

or, for pure states,

\[
x\longmapsto|\phi(x)\rangle.
\]

The cost of this transformation is part of the end-to-end complexity.

## 2. Basis encoding

A bit string can be mapped directly to a computational-basis state,

\[
x\in\{0,1\}^n
\longmapsto
|x\rangle.
\]

This uses one qubit per input bit and is simple to prepare.

## 3. Angle encoding

Features can parameterize rotations, for example

\[
|\phi(x)\rangle
=
\bigotimes_{j=1}^n R_y(x_j)|0\rangle.
\]

This uses a constant number of gates per encoded feature but generally requires a number of qubits or repeated gates related to feature dimension.

## 4. Amplitude encoding

A normalized vector \(x\in\mathbb C^d\) can be encoded as

\[
|x\rangle
=
\frac1{\|x\|}
\sum_{j=0}^{d-1}x_j|j\rangle,
\]

using only \(\lceil\log_2d\rceil\) qubits.

The compact qubit count can be misleading: generic state preparation may require resources scaling with \(d\). Algorithms assuming efficient amplitude access must state the access model explicitly, for example structured preparation or QRAM-like assumptions.

## 5. Data re-uploading

Instead of encoding data once, one may alternate data-dependent and trainable layers:

\[
U(x,\theta)
=
\prod_{\ell}
W_\ell(\theta_\ell)V_\ell(x).
\]

Repeated encoding can increase functional expressivity even with few qubits.

## 6. Quantum feature maps

A feature map defines an implicit kernel

\[
K(x,x')
=
|\langle\phi(x)|\phi(x')\rangle|^2
\]

or related overlaps. The value of a feature map therefore depends not on Hilbert-space dimension alone but on the induced geometry of the dataset and the difficulty of reproducing the relevant kernel classically.

## 7. Access models

A rigorous QML claim should distinguish

- explicit classical vectors,
- sample access,
- query/oracle access,
- coherent oracle access,
- quantum random-access memory assumptions,
- and direct quantum-state access.

Two algorithms solving “the same” statistical task under different access assumptions may not be comparable.

## 8. Encoding bottleneck

An exponential quantum state space does not automatically create an exponential feature advantage. If encoding an arbitrary \(d\)-dimensional vector requires \(O(d)\) work, the input cost may dominate a later polylogarithmic quantum subroutine.

Therefore

\[
\boxed{
\text{quantum model complexity must include data access and preparation}
}
\]

rather than counting only the trainable circuit.

## References

1. V. Havlíček et al., "Supervised learning with quantum-enhanced feature spaces," *Nature* 567, 209–212 (2019). https://doi.org/10.1038/s41586-019-0980-2
2. M. Schuld, R. Sweke, and J. J. Meyer, "Effect of data encoding on the expressive power of variational quantum-machine-learning models," *Phys. Rev. A* 103, 032430 (2021). https://doi.org/10.1103/PhysRevA.103.032430
