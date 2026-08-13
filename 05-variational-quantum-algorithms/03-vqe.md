# Variational Quantum Eigensolver

## 1. Objective

The Variational Quantum Eigensolver (VQE) estimates low-energy eigenvalues of a Hamiltonian, particularly the ground-state energy.

Given

$$
H|E_j\rangle=E_j|E_j\rangle,
$$

VQE prepares an ansatz

$$
|\psi(\boldsymbol\theta)\rangle
=U(\boldsymbol\theta)|\psi_0\rangle
$$

and minimizes

$$
E(\boldsymbol\theta)
=
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle.
$$

By the variational principle,

$$
E(\boldsymbol\theta)\ge E_0.
$$

## 2. Hamiltonian decomposition

After mapping a fermionic or physical problem to qubits, the Hamiltonian is commonly expressed as a Pauli sum,

$$
H=\sum_j c_jP_j,
$$

where $P_j$ are Pauli strings such as

$$
X\otimes Z\otimes I\otimes Y.
$$

Then

$$
E(\boldsymbol\theta)
=
\sum_j c_j\langle P_j\rangle_{\boldsymbol\theta}.
$$

The expectation values are estimated from measurements.

## 3. Measurement bottleneck

If many Pauli terms are required, naive separate estimation can be expensive. Techniques include commuting-group measurement, importance allocation, classical shadows in appropriate regimes, low-rank factorizations, and problem-specific measurement strategies.

Thus VQE complexity cannot be summarized by circuit depth alone.

## 4. Ansatz choices

Chemistry-inspired ansätze include unitary coupled-cluster constructions, while hardware-efficient ansätze prioritize native gates and shallow depth. The former use physical structure; the latter may be easier to implement but can have more difficult optimization properties.

## 5. VQE versus QPE

VQE and quantum phase estimation solve related spectral tasks through different resource tradeoffs.

**VQE:**

- repeated state preparation,
- expectation measurements,
- classical optimization,
- potentially shallower circuits.

**QPE:**

- coherent controlled evolution,
- phase extraction,
- generally deeper circuits,
- strong relevance to fault-tolerant high-precision algorithms.

Neither dominates in every resource regime.

## 6. Excited states and extensions

Extensions estimate excited states, response properties, thermal quantities, and dynamical information. These usually require additional constraints, orthogonality penalties, subspace methods, or modified cost functions.

## References

1. A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nat. Commun.* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
2. J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New J. Phys.* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
