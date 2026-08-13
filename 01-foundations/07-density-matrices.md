# Density Matrices and Mixed States

## 1. Why state vectors are not enough

A ket \(|\psi\rangle\) describes a pure state, but quantum information requires a more general representation for classical uncertainty, subsystems of entangled states, noise, and open-system dynamics. The appropriate object is the density operator.

For an ensemble \(\{p_j,|\psi_j\rangle\}\),

\[
\rho=\sum_j p_j|\psi_j\rangle\langle\psi_j|.
\]

A valid density operator satisfies

\[
\rho\succeq0,
\qquad
\operatorname{Tr}\rho=1.
\]

## 2. Pure and mixed states

A pure state has

\[
\rho=|\psi\rangle\langle\psi|,
\]

and obeys

\[
\rho^2=\rho,
\qquad
\operatorname{Tr}(\rho^2)=1.
\]

A mixed state satisfies

\[
\operatorname{Tr}(\rho^2)<1.
\]

The quantity \(\operatorname{Tr}(\rho^2)\) is called the purity.

For a qubit,

\[
\rho=\frac12(I+\mathbf r\cdot\boldsymbol\sigma),
\]

and

\[
\operatorname{Tr}(\rho^2)=\frac12(1+\|\mathbf r\|^2).
\]

## 3. Ensemble nonuniqueness

A mixed density matrix does not uniquely determine the classical ensemble used to prepare it. For example,

\[
\frac I2
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|
\]

but also

\[
\frac I2
=
\frac12|+\rangle\langle+|
+
\frac12|-\rangle\langle-|.
\]

Operational predictions depend on \(\rho\), not on a privileged ensemble decomposition.

## 4. Expectation values

For observable \(A\),

\[
\langle A\rangle=\operatorname{Tr}(\rho A).
\]

For a pure state this reduces to

\[
\langle A\rangle=\langle\psi|A|\psi\rangle.
\]

This trace form is the standard expression used throughout quantum information and variational quantum algorithms.

## 5. Reduced density operators

Given \(\rho_{AB}\), the state available to subsystem \(A\) is

\[
\rho_A=\operatorname{Tr}_B(\rho_{AB}).
\]

For a Bell pair, the joint state is pure while the local states are maximally mixed. This is not classical ignorance about a hidden local pure state; it is the operational local state induced by entanglement.

## 6. Unitary and noisy evolution

Closed evolution is

\[
\rho\mapsto U\rho U^\dagger.
\]

General physical evolution is described by a completely positive trace-preserving map (CPTP map), or quantum channel,

\[
\rho\mapsto\mathcal E(\rho).
\]

A channel can be represented in Kraus form as

\[
\mathcal E(\rho)=\sum_k K_k\rho K_k^\dagger,
\qquad
\sum_k K_k^\dagger K_k=I.
\]

This formalism will be developed further in the quantum-information-theory section.

## 7. Distance between states

Two common distinguishability measures are trace distance

\[
D(\rho,\sigma)=\frac12\|\rho-\sigma\|_1
\]

and fidelity. For a pure state \(|\psi\rangle\), one frequently uses

\[
F(|\psi\rangle,\rho)=\langle\psi|\rho|\psi\rangle.
\]

These quantities appear in state preparation, error analysis, learning, and verification.

## 8. Key takeaway

The density operator is the general representation of quantum state information. Pure kets are a special case. Once noise, discarded subsystems, or statistical mixtures appear, density matrices are the correct language.

## References

1. J. Watrous, *The Theory of Quantum Information*: https://cs.uwaterloo.ca/~watrous/TQI/
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
