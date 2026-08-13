# Entanglement Theory

## 1. From definition to resource theory

For pure bipartite states, entanglement is equivalent to non-factorizability. For mixed states, the relevant distinction is between separable and entangled density operators.

A separable state has the form

\[
\rho_{AB}
=
\sum_j p_j\rho_A^{(j)}\otimes\rho_B^{(j)}.
\]

Any state that cannot be expressed this way is entangled.

## 2. Pure-state entanglement entropy

For a bipartite pure state \(|\psi\rangle_{AB}\), the entanglement entropy is

\[
E(|\psi\rangle)
=S(\rho_A)=S(\rho_B).
\]

Using the Schmidt coefficients \(\lambda_j\),

\[
E(|\psi\rangle)
=-\sum_j\lambda_j\log\lambda_j.
\]

It vanishes exactly for product states and is maximal for maximally entangled states of fixed local dimension.

## 3. Mixed-state measures

For mixed states there is no single universally preferred entanglement measure. Examples include

- entanglement of formation,
- distillable entanglement,
- negativity,
- relative entropy of entanglement,
- and squashed entanglement.

Different measures answer different operational questions.

## 4. PPT criterion

For a bipartite state, partial transpose with respect to subsystem \(B\) is denoted

\[
\rho^{T_B}.
\]

Every separable state has positive partial transpose (PPT). For \(2\times2\) and \(2\times3\) systems, PPT is also sufficient for separability. In larger dimensions, PPT entangled states can exist.

## 5. LOCC

A central operational framework is local operations and classical communication (LOCC). Entanglement cannot be generated from separable states using LOCC alone. This motivates treating entanglement as a resource whose amount should not increase under free operations.

## 6. Distillation and dilution

Entanglement distillation converts many weakly or noisily entangled pairs into fewer high-quality entangled pairs. Entanglement dilution performs the reverse conversion. These tasks quantify operational rates and show why a resource theory needs asymptotic conversion concepts, not just static entanglement detection.

## 7. Entanglement in many-body systems and QML

Entanglement entropy and entanglement structure characterize many-body phases, tensor-network simulability, circuit complexity, and information propagation. In QML, entanglement can influence expressivity and simulation difficulty, but entanglement by itself is not a certificate of learning advantage.

## References

1. R. Horodecki et al., "Quantum entanglement," *Rev. Mod. Phys.* 81, 865 (2009). https://doi.org/10.1103/RevModPhys.81.865
2. M. B. Plenio and S. Virmani, "An introduction to entanglement measures," *Quantum Inf. Comput.* 7, 1–51 (2007). https://arxiv.org/abs/quant-ph/0504163
