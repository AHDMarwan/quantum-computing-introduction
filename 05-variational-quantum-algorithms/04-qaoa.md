# Quantum Approximate Optimization Algorithm

## 1. What QAOA is

The Quantum Approximate Optimization Algorithm (QAOA) is a gate-based variational algorithm for discrete optimization. It alternates evolution under a **cost Hamiltonian** and a **mixer Hamiltonian**, then optimizes the corresponding angles classically.

QAOA is therefore simultaneously:

- a structured parameterized quantum circuit,
- a variational quantum algorithm,
- and an optimization heuristic whose performance must be compared with strong classical methods.

## 2. Learning objectives

After this chapter, you should be able to:

- map a binary optimization objective to a diagonal Hamiltonian,
- derive the MaxCut cost Hamiltonian,
- write the depth-$p$ QAOA state,
- explain the roles of cost and mixer unitaries,
- distinguish QAOA from quantum annealing,
- explain how constraint-preserving mixers work,
- identify the meaning and cost of increasing $p$,
- distinguish approximation quality from quantum advantage,
- and analyze the classical optimization and measurement overhead.

## 3. Classical optimization problem

Suppose a problem is defined over binary strings

```math
z\in\{0,1\}^n
```

with objective

```math
C(z).
```

The goal is to find

```math
z_*
=
\arg\max_z C(z)
```

or equivalently minimize a sign-reversed objective.

QAOA encodes this classical function into a diagonal quantum operator $H_C$ satisfying

```math
H_C|z\rangle
=
C(z)|z\rangle.
```

Thus computational-basis states are candidate solutions and their eigenvalues are objective values.

## 4. MaxCut encoding

For a graph

```math
G=(V,E),
```

we assign one qubit to each vertex.

For an edge $(i,j)$, the operator

```math
C_{ij}
=
\frac12(I-Z_iZ_j)
```

has eigenvalue 1 if the two bits differ and 0 if they are equal.

Why? Since

```math
Z|0\rangle=|0\rangle,
\qquad
Z|1\rangle=-|1\rangle,
```

we have

```math
Z_iZ_j|z_i z_j\rangle
=
(-1)^{z_i+z_j}|z_i z_j\rangle.
```

If $z_i=z_j$, the eigenvalue is $+1$ and $C_{ij}=0$. If $z_i\neq z_j$, the eigenvalue is $-1$ and $C_{ij}=1$.

Therefore the MaxCut Hamiltonian is

```math
H_C
=
\frac12
\sum_{(i,j)\in E}
(I-Z_iZ_j).
```

Its expectation value is the expected cut size under measurement of the quantum state.

## 5. The mixer Hamiltonian

The standard mixer is

```math
H_M
=
\sum_{i=1}^{n}X_i.
```

The initial state is

```math
|+\rangle^{\otimes n},
```

which is the ground/eigenstate structure naturally associated with the transverse-$X$ mixer and gives uniform support over all computational-basis bit strings.

The mixer unitary is

```math
U_M(\beta)
=
e^{-i\beta H_M}.
```

Because the $X_i$ commute,

```math
U_M(\beta)
=
\prod_i e^{-i\beta X_i}.
```

## 6. Cost evolution

The cost unitary is

```math
U_C(\gamma)
=
e^{-i\gamma H_C}.
```

For MaxCut, the edge terms commute because they are diagonal in the computational basis, so

```math
U_C(\gamma)
=
\prod_{(i,j)\in E}
\exp
\left[
-i\frac\gamma2(I-Z_iZ_j)
\right].
```

Ignoring an overall phase, implementation reduces to $ZZ$ rotations on graph edges.

## 7. The depth-$p$ state

At depth $p$, define parameter vectors

```math
\boldsymbol\gamma
=(\gamma_1,\ldots,\gamma_p),
```

```math
\boldsymbol\beta
=(\beta_1,\ldots,\beta_p).
```

The QAOA state is

```math
|\boldsymbol\gamma,\boldsymbol\beta\rangle
=
\prod_{\ell=1}^{p}
U_M(\beta_\ell)
U_C(\gamma_\ell)
|+\rangle^{\otimes n}.
```

The objective is

```math
F_p(\boldsymbol\gamma,\boldsymbol\beta)
=
\langle H_C\rangle.
```

A classical optimizer seeks parameters maximizing $F_p$.

## 8. Why alternating operators can help

The cost unitary adds phases correlated with objective values. The mixer then moves amplitude between candidate bit strings.

Repeated alternation creates interference among paths through the solution space.

The intended mechanism is roughly

```text
cost-dependent phase
-> mixing between candidates
-> interference
-> higher probability on useful solutions.
```

As always, the superposition alone does not produce the optimization improvement.

## 9. Worked example: one edge

Consider a graph with two vertices and one edge.

The cost Hamiltonian is

```math
H_C
=
\frac12(I-Z_1Z_2).
```

The optimal bit strings are

```math
|01\rangle,
\qquad
|10\rangle,
```

with cost 1.

The nonoptimal strings

```math
|00\rangle,
\qquad
|11\rangle
```

have cost 0.

At $p=1$,

```math
|\gamma,\beta\rangle
=
e^{-i\beta(X_1+X_2)}
e^{-i\gamma H_C}|++\rangle.
```

Even this small example shows the QAOA logic: the cost unitary introduces a relative phase between cut and uncut sectors, and the mixer converts that phase difference into probability differences.

## 10. What does $p$ mean?

The integer $p$ controls the number of alternating cost/mixer layers.

Increasing $p$ generally increases:

- the expressivity of the ansatz,
- circuit depth,
- number of parameters,
- optimization cost,
- noise exposure.

Thus

```math
\text{larger }p
\not\Rightarrow
\text{better practical performance}.
```

In the ideal model, increasing $p$ can improve the best achievable objective value because the variational family becomes richer. But finding the optimal parameters can become harder.

## 11. Connection to adiabatic evolution

Adiabatic optimization evolves under a time-dependent Hamiltonian such as

```math
H(s)
=
(1-s)H_M+sH_C.
```

A finely discretized evolution alternates short periods under the mixer and cost Hamiltonians.

This creates a conceptual connection between QAOA and digitized adiabatic evolution.

However, finite-depth QAOA is not simply “quantum annealing with gates.” Its parameters are free variational variables rather than a fixed adiabatic schedule.

## 12. QAOA versus quantum annealing

### QAOA

```text
gate-based
parameterized discrete layers
classical optimizer
universal-circuit setting
```

### Quantum annealing

```text
continuous/scheduled Hamiltonian dynamics
optimization-oriented analog process
often specialized hardware
```

They use related Hamiltonian ideas but are distinct computational protocols.

## 13. Constraint-preserving mixers

The standard $X$ mixer explores all bit strings. But many optimization problems have constraints.

Suppose feasible solutions satisfy a constraint such as fixed Hamming weight:

```math
\sum_i z_i=k.
```

A standard $X_i$ flip leaves the feasible subspace because it changes Hamming weight.

Instead, one can design a mixer $H_M$ satisfying

```math
[H_M,Q]=0,
```

where $Q$ is the conserved constraint operator.

Then the mixer preserves feasibility.

This is an important example of ansatz design as inductive bias.

## 14. Approximation ratio

For maximization problems, performance is often summarized through an approximation ratio

```math
r
=
\frac{\mathbb E[C(z)]}{C_{\mathrm{opt}}}
```

when the objective is nonnegative and the normalization is appropriate.

But approximation ratio is only one metric. Practical optimization also cares about:

- probability of sampling the optimum,
- time to solution,
- tail quality,
- robustness across instance distributions,
- parameter-training cost.

A high expectation value does not necessarily mean the optimal solution is sampled frequently.

## 15. Classical optimization cost

QAOA requires finding

```math
\arg\max_{\boldsymbol\gamma,\boldsymbol\beta}
F_p(\boldsymbol\gamma,\boldsymbol\beta).
```

The parameter dimension is

```math
2p
```

in the standard formulation.

Although this is independent of graph size at fixed $p$, objective estimation itself becomes more expensive with problem size and hardware noise.

The optimization landscape can also exhibit symmetries, local structure, parameter concentration, or trainability problems.

## 16. Parameter transfer and structure

For related problem instances, useful parameters may transfer across:

- graph sizes,
- graph families,
- repeated local motifs,
- increasing QAOA depth.

This suggests that QAOA can be studied not only as instance-by-instance optimization but also as a learning problem over instance distributions.

That connection becomes relevant to QML and meta-optimization.

## 17. Measurement cost

For MaxCut,

```math
H_C
=
\sum_{(i,j)}C_{ij}
```

is diagonal in the computational basis.

A single sampled bit string gives a value for the entire cut objective, so measurement is relatively simple compared with a generic noncommuting Hamiltonian in VQE.

However, many samples may still be required to estimate $F_p$ precisely during optimization.

## 18. What would count as quantum advantage?

Showing that QAOA finds a good solution does not establish advantage.

The relevant comparison should include strong classical methods such as:

- approximation algorithms,
- local search,
- simulated annealing,
- semidefinite relaxations,
- message-passing methods,
- specialized heuristics,
- modern learning-assisted optimizers where relevant.

A compelling quantum result would need favorable scaling or practical performance under comparable resources on a meaningful instance distribution.

## 19. Common misconceptions

### “QAOA is a quantum version of simulated annealing.”

No. QAOA uses coherent alternating unitaries and variational parameters.

### “Increasing $p$ always improves the observed result.”

The ideal best-in-class objective may improve, but optimization and noise can make deeper circuits perform worse in practice.

### “A good approximation ratio proves quantum advantage.”

No. It must beat strong classical baselines under fair resource accounting.

### “The standard $X$ mixer is appropriate for every problem.”

No. Constraints can require problem-specific mixers.

## 20. Connections

QAOA connects:

- PQC architecture design,
- combinatorial optimization,
- adiabatic evolution,
- constraint-preserving dynamics,
- classical parameter optimization,
- and approximation theory.

It also illustrates a general QML lesson: **architecture should encode structure rather than merely maximize expressibility**.

## 21. Exercises

### Conceptual

1. Explain why the MaxCut cost Hamiltonian is diagonal in the computational basis.
2. Why does the mixer need to fail to commute with the cost Hamiltonian to generate nontrivial dynamics?
3. Explain why constraint-preserving mixers can improve search efficiency.
4. Why is $p$ simultaneously a representation and hardware resource?

### Computational

5. Verify the eigenvalues of

```math
\frac12(I-Z_iZ_j)
```

on all four two-qubit computational-basis states.
6. Show that the terms $X_i$ in the standard mixer commute with one another.
7. For a triangle graph, write the MaxCut Hamiltonian explicitly.
8. Given a measured bit string for a graph, show how its cut value can be computed classically without separately measuring each edge term.

### Research-oriented

9. Design a fair benchmark comparing QAOA with a classical heuristic. What resources and instance distribution must be fixed?
10. How could parameter transfer across graph sizes be interpreted as a learning problem?
11. When could a highly constrained mixer outperform a more expressive unconstrained mixer?
12. What evidence would distinguish a genuine QAOA advantage from poor classical baseline selection?

## 22. Key takeaways

- QAOA alternates cost-dependent phase evolution with mixing dynamics.
- The cost Hamiltonian encodes classical objective values as eigenvalues.
- The mixer controls movement through the candidate-solution space.
- Depth $p$ increases representation power but also circuit and optimization cost.
- Problem-specific mixers can preserve constraints and encode useful inductive bias.
- QAOA and quantum annealing are related but distinct.
- Approximation quality alone does not establish quantum advantage.

## References

1. E. Farhi, J. Goldstone, and S. Gutmann, "A Quantum Approximate Optimization Algorithm." https://arxiv.org/abs/1411.4028
2. S. Hadfield et al., "From the Quantum Approximate Optimization Algorithm to a Quantum Alternating Operator Ansatz," *Algorithms* 12, 34 (2019). https://doi.org/10.3390/a12020034
3. M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
