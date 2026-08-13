# Quantum Approximate Optimization Algorithm

## 1. Problem setting

The Quantum Approximate Optimization Algorithm (QAOA) is a gate-based variational algorithm for discrete optimization. A classical cost function is encoded into a diagonal cost Hamiltonian $H_C$.

For MaxCut on graph $G=(V,E)$, one can use

$$
H_C
=
\frac12\sum_{(i,j)\in E}(I-Z_iZ_j).
$$

Its expectation corresponds to cut quality.

## 2. Alternating ansatz

A standard mixer is

$$
H_M=\sum_i X_i.
$$

At depth $p$, the QAOA state is

$$
|\boldsymbol\gamma,\boldsymbol\beta\rangle
=
\prod_{\ell=1}^{p}
 e^{-i\beta_\ell H_M}
 e^{-i\gamma_\ell H_C}
|+\rangle^{\otimes n}.
$$

The parameters are optimized to maximize

$$
\langle H_C\rangle.
$$

## 3. What $p$ means

The integer $p$ is the number of alternating cost/mixer layers. Increasing $p$ enlarges the variational family and generally increases circuit depth and optimization difficulty.

In the ideal limit, suitable QAOA constructions connect conceptually with adiabatic evolution, but finite-depth QAOA is a distinct variational algorithm.

## 4. Mixers and constraints

The standard $X$-mixer explores the full binary space. For constrained optimization, alternative mixers can preserve feasibility subspaces. This is an example of encoding problem structure directly into the ansatz.

## 5. Approximation and advantage

QAOA quality must be judged against strong classical approximation and heuristic algorithms. Showing that QAOA produces a good cut does not establish quantum advantage; the relevant question is whether it achieves a superior quality-resource scaling on a meaningful problem distribution.

## 6. QAOA versus annealing

QAOA uses discrete parameterized unitary layers and a classical optimizer. Quantum annealing uses continuous or scheduled Hamiltonian evolution in an optimization-oriented physical process. They share Hamiltonian ideas but are not the same computational protocol.

## References

1. E. Farhi, J. Goldstone, and S. Gutmann, "A Quantum Approximate Optimization Algorithm" (2014). https://arxiv.org/abs/1411.4028
2. S. Hadfield et al., "From the Quantum Approximate Optimization Algorithm to a Quantum Alternating Operator Ansatz," *Algorithms* 12, 34 (2019). https://doi.org/10.3390/a12020034
