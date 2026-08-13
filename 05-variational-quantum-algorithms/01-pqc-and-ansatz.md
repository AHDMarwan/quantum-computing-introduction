# Parameterized Quantum Circuits and Ansätze

## 1. Parameterized quantum circuit

A parameterized quantum circuit (PQC) is a circuit whose unitary depends on continuous or discrete parameters,

\[
U(\boldsymbol\theta)
=U_L(\theta_L)\cdots U_1(\theta_1).
\]

For an initial state \(|\psi_0\rangle\), the circuit prepares

\[
|\psi(\boldsymbol\theta)\rangle
=U(\boldsymbol\theta)|\psi_0\rangle.
\]

“PQC” describes the computational object. It does not specify the task, the loss, or even whether the parameters are optimized.

## 2. Ansatz

An ansatz is a chosen family of candidate states or transformations. For state preparation,

\[
\mathcal A
=
\{U(\boldsymbol\theta)|\psi_0\rangle:\boldsymbol\theta\in\Theta\}.
\]

The term expresses a modeling assumption: the desired solution is expected to lie in, or be approximated by, the family.

A PQC is a common implementation of an ansatz, but conceptually

\[
\text{ansatz} = \text{hypothesis family},
\qquad
\text{PQC} = \text{circuit realization}.
\]

## 3. Hardware-efficient ansätze

A hardware-efficient ansatz typically alternates local parameterized rotations with native entangling layers:

\[
U(\boldsymbol\theta)
=
\prod_{\ell=1}^L
U_{\rm ent}^{(\ell)}
U_{\rm local}^{(\ell)}(\boldsymbol\theta_\ell).
\]

These circuits can be shallow and compatible with device connectivity, but their trainability and symmetry properties must be analyzed rather than assumed.

## 4. Problem-inspired ansätze

Problem-inspired circuits encode known structure. Examples include particle-number-preserving circuits for chemistry and QAOA-style alternating operators for combinatorial optimization.

The tradeoff is often

\[
\text{more prior structure}
\longleftrightarrow
\text{smaller but better-aligned hypothesis space}.
\]

## 5. Expressibility is not sufficient

An ansatz capable of approximating many states may appear desirable, but excessive expressibility can produce concentration phenomena and difficult optimization landscapes. The design goals include not only representation, but also

- trainability,
- symmetry preservation,
- noise robustness,
- measurement cost,
- and resource efficiency.

## 6. Data-dependent PQCs

In QML one frequently uses

\[
U(x,\boldsymbol\theta),
\]

where \(x\) encodes data and \(\boldsymbol\theta\) are trainable parameters. Data can appear in a separate feature map or be repeatedly re-uploaded throughout the circuit.

This remains a PQC, but its role is now a learning-model component.

## References

1. M. Cerezo et al., "Variational quantum algorithms," *Nat. Rev. Phys.* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
2. A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nat. Commun.* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
