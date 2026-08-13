# Quantum Entropy and Information

## 1. Von Neumann entropy

The quantum analogue of Shannon entropy is the von Neumann entropy

\[
S(\rho)
=-\operatorname{Tr}(\rho\log\rho).
\]

If \(\rho\) has eigenvalues \(\lambda_i\), then

\[
S(\rho)=-\sum_i\lambda_i\log\lambda_i.
\]

Pure states have \(S(\rho)=0\). A maximally mixed state on dimension \(d\),

\[
\rho=\frac{I}{d},
\]

has entropy \(\log d\).

## 2. Joint and conditional entropy

For a bipartite state \(\rho_{AB}\),

\[
S(A)=S(\rho_A),
\qquad
S(B)=S(\rho_B),
\qquad
S(AB)=S(\rho_{AB}).
\]

Quantum conditional entropy is

\[
S(A|B)=S(AB)-S(B).
\]

Unlike its classical counterpart, it can be negative. For a maximally entangled pure state, \(S(AB)=0\) while \(S(B)>0\), so

\[
S(A|B)<0.
\]

This is a genuinely quantum information-theoretic phenomenon.

## 3. Mutual information

Quantum mutual information is

\[
I(A:B)
=S(A)+S(B)-S(AB).
\]

It quantifies total correlations, including both classical and quantum correlations.

An equivalent expression is a relative entropy:

\[
I(A:B)
=D(\rho_{AB}\|\rho_A\otimes\rho_B).
\]

## 4. Quantum relative entropy

For suitable supports,

\[
D(\rho\|\sigma)
=
\operatorname{Tr}\big[\rho(\log\rho-\log\sigma)\big].
\]

Relative entropy is not a symmetric distance, but it is fundamental in hypothesis testing, channel capacities, thermodynamic resource theories, and learning theory.

A crucial property is data processing:

\[
D(\rho\|\sigma)
\ge
D(\mathcal E(\rho)\|\mathcal E(\sigma))
\]

for every quantum channel \(\mathcal E\). Physical processing cannot increase distinguishability as quantified by relative entropy.

## 5. Holevo information

For an ensemble \(\{p_x,\rho_x\}\), define

\[
\bar\rho=\sum_x p_x\rho_x.
\]

The Holevo quantity is

\[
\chi
=S(\bar\rho)-\sum_xp_xS(\rho_x).
\]

It bounds the amount of classical information accessible through measurement from a quantum ensemble. This formalizes why a quantum state with a large Hilbert-space dimension cannot simply be “read out” as all of its amplitudes.

## 6. Entropy in learning

Entropy and mutual information appear in

- representation learning,
- information bottlenecks,
- quantum state discrimination,
- generalization bounds,
- feature selection,
- and resource quantification.

A quantum learning model may be designed around operational information quantities rather than only scalar prediction losses.

## References

1. J. von Neumann, *Mathematical Foundations of Quantum Mechanics*.
2. A. S. Holevo, "Bounds for the quantity of information transmitted by a quantum communication channel," *Problems of Information Transmission* 9 (1973).
3. J. Watrous, *The Theory of Quantum Information*: https://cs.uwaterloo.ca/~watrous/TQI/
