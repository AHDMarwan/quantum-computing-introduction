# Quantum Channels

## 1. General physical transformations

Closed quantum evolution is unitary, but realistic systems interact with environments, lose information, undergo measurement, and experience noise. The general deterministic transformation of a quantum state is a **completely positive trace-preserving** (CPTP) linear map

\[
\mathcal E:\mathcal L(\mathcal H_A)\to\mathcal L(\mathcal H_B).
\]

For every density operator \(\rho\), \(\mathcal E(\rho)\) must again be a valid density operator.

## 2. Why complete positivity?

Positivity requires

\[
\rho\succeq0\Rightarrow\mathcal E(\rho)\succeq0.
\]

Complete positivity is stronger: for every auxiliary dimension \(k\),

\[
\mathcal E\otimes I_k
\]

must also preserve positivity. This is necessary because the input system may be entangled with an untouched reference system.

## 3. Kraus representation

Every finite-dimensional quantum channel can be written

\[
\mathcal E(\rho)
=
\sum_k K_k\rho K_k^\dagger,
\]

with

\[
\sum_k K_k^\dagger K_k=I.
\]

The Kraus representation is not unique.

Examples include depolarizing noise, dephasing, amplitude damping, erasure, and measurement channels.

## 4. Stinespring dilation

Every quantum channel can be represented as unitary evolution on a larger system followed by discarding an environment:

\[
\mathcal E(\rho)
=
\operatorname{Tr}_E
\left[
U(\rho\otimes|0\rangle\langle0|_E)U^\dagger
\right].
\]

This explains how apparently irreversible open-system dynamics can emerge from reversible evolution on a larger Hilbert space.

## 5. Choi representation

A linear map can be represented by its Choi operator. For input dimension \(d\), define a maximally entangled state

\[
|\Phi\rangle
=\frac1{\sqrt d}\sum_{j=1}^d|j\rangle|j\rangle.
\]

The Choi state/operator is proportional to

\[
J(\mathcal E)
=(\mathcal E\otimes I)(|\Phi\rangle\langle\Phi|).
\]

Complete positivity corresponds to positivity of the Choi operator, and trace preservation imposes a partial-trace constraint. This representation is central in process tomography, channel discrimination, and learning quantum processes.

## 6. Composition and tensor products

Sequential channels compose as

\[
\mathcal E_2\circ\mathcal E_1,
\]

while independent systems use

\[
\mathcal E_A\otimes\mathcal E_B.
\]

Noisy quantum circuits are therefore compositions of ideal and noisy channels rather than a single unitary matrix.

## 7. Channels in QML

A variational model need not be unitary. It can be a parameterized channel

\[
\rho\mapsto\mathcal E_{\boldsymbol\theta}(\rho),
\]

including dissipation, mid-circuit measurement, reset, and environment-assisted dynamics. This broader viewpoint is important when questioning the assumption that a trainable quantum model must be a unitary PQC.

## References

1. J. Watrous, *The Theory of Quantum Information*, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
2. K. Kraus, *States, Effects, and Operations*, Springer, 1983.
3. W. F. Stinespring, "Positive Functions on C*-Algebras," *Proc. AMS* 6, 211–216 (1955). https://doi.org/10.1090/S0002-9939-1955-0069403-4
