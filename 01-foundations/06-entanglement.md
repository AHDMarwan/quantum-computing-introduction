# Entanglement

## 1. Definition

A pure bipartite state $|\psi\rangle_{AB}$ is **separable** if there exist states $|a\rangle_A$ and $|b\rangle_B$ such that

$$
|\psi\rangle_{AB}=|a\rangle_A\otimes|b\rangle_B.
$$

If no such factorization exists, the state is entangled.

The canonical example is the Bell state

$$
|\Phi^+\rangle=\frac{|00\rangle+|11\rangle}{\sqrt2}.
$$

It is a pure state of the pair, but neither qubit has a pure local state.

## 2. Reduced states

For

$$
\rho_{AB}=|\Phi^+\rangle\langle\Phi^+|,
$$

the reduced states are

$$
\rho_A=\operatorname{Tr}_B\rho_{AB}=\frac I2,
\qquad
\rho_B=\frac I2.
$$

Thus complete knowledge of the joint state does not imply a pure state for each part. The information can reside in correlations.

## 3. Schmidt decomposition

Every bipartite pure state can be written

$$
|\psi\rangle
=
\sum_{k=1}^r \sqrt{\lambda_k}
|u_k\rangle_A|v_k\rangle_B,
$$

where $\lambda_k\ge0$, $\sum_k\lambda_k=1$, and $\{|u_k\rangle\}$, $\{|v_k\rangle\}$ are orthonormal sets.

The state is separable iff the Schmidt rank is one. For a bipartite pure state, the reduced density operators have eigenvalues $\lambda_k$, so the entanglement entropy is

$$
S(\rho_A)=S(\rho_B)
=-\sum_k\lambda_k\log\lambda_k.
$$

## 4. Correlation is not automatically entanglement

The mixed state

$$
\rho
=
\frac12|00\rangle\langle00|
+
\frac12|11\rangle\langle11|
$$

has strong classical correlations but is separable because it is a convex mixture of product states. Therefore correlation and entanglement are different concepts.

For mixed states, separability means

$$
\rho_{AB}
=
\sum_j p_j\rho_A^{(j)}\otimes\rho_B^{(j)}.
$$

Determining separability is generally much harder than checking pure-state factorization.

## 5. Bell nonlocality

Entanglement can produce correlations incompatible with local hidden-variable models. Bell inequalities make this statement operational. However,

$$
\text{Bell nonlocality}
\neq
\text{entanglement}
$$

as mathematical sets for general mixed states: every Bell-nonlocal state is entangled, but not every entangled mixed state violates a given Bell inequality.

## 6. Entanglement as a resource

Entanglement enables protocols such as teleportation and superdense coding and is central to quantum communication and many-body physics. In quantum computing it is often necessary for strong nonclassical correlations, but the presence of entanglement alone does not prove a computational speedup.

Resource questions require specifying

- the task,
- the allowed operations,
- the entanglement measure,
- and the classical or restricted competitor.

This viewpoint leads naturally to quantum resource theories.

## 7. Entanglement in QML

QML papers often associate more entanglement with greater expressivity. That relationship is not monotonic. Excessive expressivity or random-like circuits can harm trainability, and classically simulable structures can contain substantial entanglement in restricted forms. Therefore entanglement should be treated as one structural property, not as a synonym for quantum advantage.

## References

1. R. Horodecki et al., "Quantum entanglement," *Rev. Mod. Phys.* 81, 865 (2009). https://doi.org/10.1103/RevModPhys.81.865
2. J. S. Bell, "On the Einstein Podolsky Rosen paradox," *Physics Physique Fizika* 1, 195 (1964). https://doi.org/10.1103/PhysicsPhysiqueFizika.1.195
3. C. H. Bennett et al., "Teleporting an unknown quantum state via dual classical and EPR channels," *Phys. Rev. Lett.* 70, 1895 (1993). https://doi.org/10.1103/PhysRevLett.70.1895
