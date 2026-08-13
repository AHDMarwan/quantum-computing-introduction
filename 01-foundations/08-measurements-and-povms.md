# Measurements and POVMs

## 1. Measurement as an interface

A quantum state is not directly readable as a list of amplitudes. Measurement produces classical outcomes according to probabilities determined jointly by the state and the measurement. This state-measurement duality is essential in quantum algorithms, communication, sensing, and QML.

## 2. Projective measurement

Let

\[
A=\sum_a aP_a
\]

be a spectral decomposition with orthogonal projectors \(P_a\). Measuring \(A\) on state \(\rho\) gives outcome \(a\) with probability

\[
p(a)=\operatorname{Tr}(P_a\rho).
\]

For a pure state,

\[
p(a)=\langle\psi|P_a|\psi\rangle.
\]

The expectation value is

\[
\mathbb E[A]
=
\sum_a a\,p(a)
=
\operatorname{Tr}(A\rho).
\]

## 3. Computational-basis measurement

For one qubit,

\[
P_0=|0\rangle\langle0|,
\qquad
P_1=|1\rangle\langle1|.
\]

If

\[
|\psi\rangle=\alpha|0\rangle+\beta|1\rangle,
\]

then

\[
p(0)=|\alpha|^2,
\qquad
p(1)=|\beta|^2.
\]

For an \(n\)-qubit state, computational-basis sampling returns a bit string \(z\in\{0,1\}^n\).

## 4. General measurements: POVMs

A positive-operator-valued measure is a collection of positive semidefinite operators

\[
\{E_y\}_y
\]

satisfying

\[
E_y\succeq0,
\qquad
\sum_y E_y=I.
\]

The probability of outcome \(y\) is

\[
p(y)=\operatorname{Tr}(E_y\rho).
\]

POVM elements need not be orthogonal projectors. This extra freedom is important in optimal state discrimination and information extraction.

## 5. POVMs versus measurement instruments

A POVM specifies outcome probabilities but does not fully specify the post-measurement state. A **quantum instrument** provides both the classical outcome and the conditional state transformation. If \(\mathcal I_y\) is the operation associated with outcome \(y\), then

\[
p(y)=\operatorname{Tr}[\mathcal I_y(\rho)],
\]

and the normalized post-measurement state is

\[
\rho_y
=
\frac{\mathcal I_y(\rho)}{p(y)}.
\]

This distinction becomes important for adaptive protocols and sequential learning.

## 6. Noncommuting observables

If

\[
[A,B]\neq0,
\]

then the two observables generally do not share a complete eigenbasis. Quantum theory therefore lacks a single classical joint assignment reproducing all measurement contexts in the naive way.

For Pauli matrices,

\[
[X,Z]\neq0.
\]

An eigenstate of \(Z\) is not an eigenstate of \(X\). This incompatibility is a structural resource in quantum information.

## 7. Sampling and shot noise

A real quantum processor estimates expectation values from a finite number \(N\) of measurement shots. For a bounded observable, the empirical estimator has statistical uncertainty scaling generically as

\[
O(N^{-1/2}).
\]

Thus measurement cost is part of quantum-algorithm complexity. In variational algorithms and QML, a model evaluation is not an exact floating-point function call; it is often a statistical estimation procedure.

## 8. State discrimination

Suppose a state is drawn from an ensemble \(\{p_x,\rho_x\}\). A measurement \(\{E_y\}\) is chosen to infer \(x\). Optimizing the measurement gives a decision-theoretic problem over POVMs. This is one of the clearest examples where the measurement itself is a computational or learning object rather than a passive final readout.

## 9. Key takeaway

Quantum measurement is not simply “looking at a state.” It is a selectable physical operation that converts quantum information into classical data. Projective measurements are a special case; POVMs describe the most general outcome statistics, and instruments describe the corresponding state update.

## References

1. J. Watrous, *The Theory of Quantum Information*: https://cs.uwaterloo.ca/~watrous/TQI/
2. C. W. Helstrom, *Quantum Detection and Estimation Theory*, Academic Press, 1976.
3. A. S. Holevo, *Probabilistic and Statistical Aspects of Quantum Theory*, 1982.
