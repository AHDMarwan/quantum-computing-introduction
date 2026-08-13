# Variational Quantum Eigensolver

## 1. Objective

The Variational Quantum Eigensolver (VQE) is a hybrid algorithm for estimating low-energy eigenvalues of a Hermitian Hamiltonian, especially the ground-state energy.

Given

```math
H|E_j\rangle=E_j|E_j\rangle,
```

VQE prepares

```math
|\psi(\boldsymbol\theta)\rangle
=
U(\boldsymbol\theta)|\psi_0\rangle
```

and minimizes

```math
E(\boldsymbol\theta)
=
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle.
```

By the variational principle,

```math
E(\boldsymbol\theta)\ge E_0.
```

## 2. Learning objectives

After this chapter, you should be able to:

- derive the VQE objective from the variational principle,
- explain how physical Hamiltonians are mapped to qubit observables,
- decompose a Hamiltonian into Pauli strings,
- reconstruct energy from measured expectation values,
- identify measurement variance as a major resource,
- distinguish chemistry-inspired and hardware-efficient ansätze,
- separate ansatz, optimizer, sampling, and hardware errors,
- compare VQE with QPE,
- and audit a VQE advantage claim using end-to-end resource accounting.

## 3. From a physical problem to a qubit Hamiltonian

In quantum chemistry or lattice models, the original Hamiltonian may be expressed in fermionic or other physical operators. A mapping converts it to a qubit operator of the form

```math
H
=
\sum_{j=1}^{M}c_jP_j,
```

where each $P_j$ is a Pauli string,

```math
P_j
\in
\{I,X,Y,Z\}^{\otimes n}.
```

Examples include

```math
Z_1Z_2,
\qquad
X_1Y_2Z_4,
\qquad
I.
```

The coefficients $c_j$ are real because $H$ is Hermitian.

## 4. Energy estimation

Linearity gives

```math
E(\boldsymbol\theta)
=
\sum_jc_j
\langle P_j\rangle_{\boldsymbol\theta}.
```

Thus VQE does not measure the full Hamiltonian in one shot. It estimates the expectation values of the terms needed to reconstruct the energy.

For each Pauli string,

```math
\langle P_j\rangle_{\boldsymbol\theta}
=
\langle\psi(\boldsymbol\theta)|P_j|\psi(\boldsymbol\theta)\rangle.
```

Each estimate comes from repeated measurements after rotating into the appropriate basis.

## 5. Worked example: two-term Hamiltonian

Consider

```math
H
=
aZ+bX.
```

Use the one-qubit ansatz

```math
|\psi(\theta)\rangle
=
R_y(\theta)|0\rangle.
```

For this state,

```math
\langle Z\rangle=\cos\theta,
```

and

```math
\langle X\rangle=\sin\theta.
```

Therefore

```math
E(\theta)
=
a\cos\theta+b\sin\theta.
```

This can be minimized analytically. Writing

```math
R=\sqrt{a^2+b^2},
```

we can express

```math
E(\theta)
=
R\cos(\theta-\phi)
```

for an appropriate phase $\phi$. The minimum is

```math
E_{\min}=-R.
```

This equals the lowest eigenvalue of $aZ+bX$, showing that the ansatz is expressive enough for this one-qubit problem.

## 6. Measurement variance

Suppose

```math
H=\sum_jc_jP_j.
```

If each $P_j$ is estimated independently using $N_j$ shots, an approximate energy-estimator variance is

```math
\mathrm{Var}(\widehat E)
=
\sum_j
c_j^2
\frac{1-\langle P_j\rangle^2}{N_j},
```

when covariance between separately measured groups is absent.

This equation shows why shot allocation matters. Terms with large coefficients or large intrinsic variance deserve more measurement effort.

## 7. Measurement grouping

Pauli terms that are compatible can sometimes be measured in the same circuit setting.

If $P_j$ and $P_k$ commute, there may exist a common measurement basis. Grouping commuting terms can reduce the number of distinct circuit settings.

But several notions of compatibility exist. Pairwise commutation alone does not always imply that a simple tensor-product measurement basis is sufficient.

Measurement optimization is therefore a nontrivial part of VQE implementation.

## 8. Measurement cost as a bottleneck

A Hamiltonian may contain many terms. Even if one ansatz circuit is shallow, the algorithm may require

```math
N_{\mathrm{iter}}
\times
N_{\mathrm{groups}}
\times
N_{\mathrm{shots}}
```

circuit executions.

This is why VQE complexity cannot be summarized by “circuit depth.”

Techniques for reducing measurement cost include:

- commuting-group strategies,
- adaptive shot allocation,
- low-rank decompositions,
- basis-rotation methods,
- and classical-shadow-style approaches in suitable regimes.

No single strategy dominates for all Hamiltonians.

## 9. Ansatz choices

### Hardware-efficient ansatz

A hardware-efficient ansatz uses native rotations and entanglers.

Advantages:

- shallow compiled circuits,
- simple device execution.

Risks:

- weak physical inductive bias,
- symmetry leakage,
- trainability problems at depth.

### Problem-inspired ansatz

Chemistry-inspired ansätze incorporate physical structure, for example excitation operators and particle-number constraints.

Advantages:

- stronger connection to the target state,
- potentially smaller relevant search space.

Risks:

- deeper circuits,
- costly operator decompositions,
- difficult implementation on restricted hardware.

The relevant comparison is not “which ansatz is more expressive?” but rather

```text
representation quality
vs
trainability
vs
circuit cost
vs
measurement cost.
```

## 10. Initial-state preparation

VQE usually starts from a reference state $|\psi_0\rangle$.

In chemistry, a mean-field reference may already have substantial overlap with the exact ground state. A good reference can reduce the burden placed on the variational circuit.

If the initial state is poor, the ansatz may need greater depth or more difficult optimization.

Thus state preparation and ansatz design should be analyzed together.

## 11. Error decomposition

The final energy error can be viewed schematically as

```math
\Delta E
\approx
\Delta_{\mathrm{mapping}}
+
\Delta_{\mathrm{ansatz}}
+
\Delta_{\mathrm{optimization}}
+
\Delta_{\mathrm{sampling}}
+
\Delta_{\mathrm{hardware}}.
```

Depending on the application, additional approximations may enter through basis truncation or model reduction before the quantum algorithm even begins.

A VQE experiment that misses the exact energy does not automatically diagnose which component failed.

## 12. Chemical accuracy is not a universal metric

In molecular applications, one often discusses a target energy precision motivated by chemistry. But useful accuracy depends on the physical quantity being predicted.

Energy differences, reaction barriers, forces, excited-state gaps, and response properties can have different error requirements.

Therefore one should define the operational scientific target before quoting “success.”

## 13. Optimization landscape

VQE optimization can be difficult because of:

- nonconvexity,
- local minima or saddle structure,
- finite-shot noise,
- barren plateaus,
- parameter redundancy,
- hardware bias.

A good final energy does not imply the optimization landscape was easy; conversely, a poor result may reflect optimizer failure rather than a quantum-representation limitation.

## 14. VQE versus QPE

VQE and QPE estimate spectral information using very different resources.

### VQE

```text
prepare parameterized state
-> measure many expectation values
-> classical optimization
-> repeat
```

Potential strengths:

- shallower coherent circuits,
- flexible ansatz design,
- compatibility with hybrid workflows.

Potential weaknesses:

- many repeated measurements,
- difficult optimization,
- no generic guarantee of reaching the exact eigenstate.

### QPE

```text
prepare state with eigenstate overlap
-> controlled long-time evolution
-> phase extraction
```

Potential strengths:

- direct spectral estimation,
- systematic precision scaling in fault-tolerant regimes.

Potential weaknesses:

- long coherent depth,
- demanding controlled simulation,
- dependence on initial-state overlap.

The better method depends on the hardware regime and target precision.

## 15. Excited states

The basic variational principle targets the lowest eigenvalue. Excited-state methods require additional structure, such as:

- orthogonality penalties,
- subspace diagonalization,
- deflation,
- symmetry selection,
- state-averaged objectives.

For example, one can penalize overlap with an already found state $|\psi_0\rangle$:

```math
C_1(\theta)
=
\langle H\rangle_\theta
+
\beta
|\langle\psi_0|\psi(\theta)\rangle|^2.
```

The penalty parameter $\beta$ must be chosen carefully.

## 16. Does VQE provide quantum advantage?

Running VQE on a quantum processor is not itself evidence of quantum advantage.

A meaningful claim must compare against strong classical methods for the same physical regime, including methods that exploit:

- low entanglement,
- sparsity,
- perturbative structure,
- tensor networks,
- coupled-cluster approximations,
- quantum Monte Carlo where applicable,
- problem-specific chemistry algorithms.

The relevant question is whether the complete quantum workflow offers a favorable scaling or practical frontier in a regime where classical methods fail.

## 17. Resource accounting

A VQE resource estimate should include at least:

```text
logical/physical qubits
circuit depth per ansatz evaluation
number of Hamiltonian terms or groups
shots per group
number of optimization iterations
gradient or objective evaluations
state-preparation cost
error mitigation overhead
classical optimization cost
```

A useful abstract model is

```math
C_{\mathrm{VQE}}
\sim
N_{\mathrm{iter}}
N_{\mathrm{settings/iter}}
N_{\mathrm{shots/setting}}
C_{\mathrm{circuit}}.
```

## 18. Common misconceptions

### “VQE solves the eigenvalue problem because of the variational principle.”

The variational principle gives a bound. Success still depends on ansatz quality and optimization.

### “A low circuit depth means VQE is cheap.”

Measurement and optimization can require very many circuit executions.

### “Hardware-efficient ansätze are always preferable on hardware.”

Not if they create a badly aligned or untrainable hypothesis class.

### “VQE is always the near-term replacement for QPE.”

They are different resource tradeoffs, not a universal chronological hierarchy.

## 19. Connections

VQE links together:

- the variational principle,
- PQC ansatz design,
- quantum measurement,
- classical optimization,
- gradient estimation,
- barren plateaus,
- and quantum simulation.

These same components reappear in variational QML.

## 20. Exercises

### Conceptual

1. Why does VQE return an upper bound to the ground energy in the ideal setting?
2. Why is measurement cost independent from ansatz depth?
3. Explain how a symmetry-preserving ansatz can reduce wasted search space.
4. Why can a good classical reference state reduce quantum circuit requirements?

### Computational

5. For $H=aZ+bX$, derive the exact minimum of the worked-example cost.
6. Suppose $H=0.8Z+0.2X$ and each term receives 1000 shots. Write the estimator variance in terms of the two expectation values.
7. Given coefficients $c_1=10$ and $c_2=1$, explain qualitatively why equal shot allocation may be inefficient.
8. For a Hamiltonian $H=c_0I+c_1Z_1+c_2Z_2+c_3Z_1Z_2$, identify a measurement basis that estimates all nonidentity terms in one setting.

### Research-oriented

9. Design an experiment that separates ansatz error from optimizer error in VQE.
10. A VQE paper reports energy accuracy but omits total shot count. Why is comparison with a classical solver incomplete?
11. When could a classically simulable ansatz still be scientifically useful in VQE?
12. What evidence would be required to argue for a genuine VQE advantage rather than a successful quantum demonstration?

## 21. Key takeaways

- VQE minimizes a Hamiltonian expectation value over a parameterized state family.
- Hamiltonian decomposition turns energy estimation into many observable-estimation problems.
- Measurement cost, ansatz quality, and optimization are all central resources.
- The variational principle provides a bound but does not guarantee convergence to the exact ground state.
- VQE and QPE occupy different resource regimes.
- Quantum advantage requires comparison with strong structure-aware classical methods and complete resource accounting.

## References

1. A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nature Communications* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
2. J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New Journal of Physics* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
3. M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
