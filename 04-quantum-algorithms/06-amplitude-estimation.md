# Quantum Amplitude Estimation

## 1. Problem

Suppose a unitary \(A\) prepares

\[
A|0\rangle
=
\sqrt{1-a}\,|\psi_0\rangle|0\rangle
+
\sqrt a\,|\psi_1\rangle|1\rangle,
\]

where \(a\in[0,1]\) is an unknown probability of interest. Amplitude estimation seeks to estimate \(a\).

## 2. Quadratic precision improvement

Classical Monte Carlo estimation of a probability to additive error \(\epsilon\) requires

\[
O(1/\epsilon^2)
\]

independent samples in the standard setting. Ideal quantum amplitude estimation can achieve

\[
O(1/\epsilon)
\]

uses of coherent state-preparation/reflection primitives, giving a quadratic query-complexity improvement.

## 3. Relation to Grover rotations

As in amplitude amplification, define an angle \(\theta\) such that

\[
a=\sin^2\theta.
\]

A Grover-like operator acts as a rotation whose eigenphases encode \(\theta\). Original amplitude estimation applies phase estimation to this operator and then converts the estimated phase into \(a\).

## 4. Modern variants

The original algorithm requires deep coherent phase-estimation circuitry. Later variants trade circuit depth, adaptivity, classical postprocessing, and sampling complexity differently. This is important when comparing NISQ-style implementations with fault-tolerant algorithms.

## 5. Applications

Potential applications include

- Monte Carlo integration,
- risk estimation,
- option pricing,
- expectation estimation,
- and probabilistic subroutines inside larger algorithms.

The practical value depends on whether the probability distribution and payoff function can be loaded coherently at acceptable cost.

## 6. Input-loading caveat

A formal \(O(1/\epsilon)\) oracle complexity does not automatically yield an end-to-end quadratic speedup if preparing \(A\), implementing reflections, or loading classical distributions dominates the cost. Access assumptions must therefore be explicit.

## References

1. G. Brassard et al., "Quantum Amplitude Amplification and Estimation," *Contemporary Mathematics* 305, 53–74 (2002). https://arxiv.org/abs/quant-ph/0005055
