# Variational Principle and the Hybrid Quantum–Classical Loop

## 1. Why variational algorithms are hybrid

A variational quantum algorithm (VQA) combines two different computational resources:

```text
quantum state preparation + measurement
<->
classical parameter optimization
```

The quantum processor evaluates information about a parameterized state, while the classical controller decides how parameters should change.

This is an algorithmic framework, not a single algorithm.

## 2. Learning objectives

After this chapter, you should be able to:

- define the generic VQA loop,
- explain the roles of the quantum and classical components,
- derive the variational upper bound for ground-state energy,
- distinguish exact costs from finite-shot estimators,
- decompose total VQA error into representation, optimization, sampling, and hardware contributions,
- identify stopping criteria and optimization failure modes,
- and analyze total training cost rather than circuit depth alone.

## 3. Generic VQA structure

Let

```math
|\psi(\boldsymbol\theta)\rangle
=
U(\boldsymbol\theta)|\psi_0\rangle.
```

A cost function is defined as

```math
C(\boldsymbol\theta).
```

Often it is an expectation value,

```math
C(\boldsymbol\theta)
=
\langle\psi(\boldsymbol\theta)|O|\psi(\boldsymbol\theta)\rangle.
```

The optimizer produces a sequence

```math
\boldsymbol\theta_0,
\boldsymbol\theta_1,
\boldsymbol\theta_2,
\ldots
```

according to measured cost or gradient information.

A generic update can be written

```math
\boldsymbol\theta_{t+1}
=
\mathcal O
\left(
\boldsymbol\theta_t,
\widehat C_t,
\widehat{\nabla C}_t,
\ldots
\right).
```

The hats matter because quantum hardware normally returns statistical estimates rather than exact real numbers.

## 4. The quantum component

At iteration $t$, the quantum device typically performs:

1. state preparation,
2. parameterized evolution,
3. measurement in one or more bases,
4. repeated shots to estimate observables.

For example,

```math
\widehat C_t
\approx
\langle O\rangle_{\boldsymbol\theta_t}.
```

If the observable decomposes as

```math
O
=
\sum_j c_jP_j,
```

then the cost is reconstructed from estimates of the individual terms:

```math
C(\boldsymbol\theta)
=
\sum_j c_j
\langle P_j\rangle_{\boldsymbol\theta}.
```

## 5. The classical component

The classical computer may perform:

- parameter updates,
- gradient reconstruction,
- line search,
- momentum or adaptive optimization,
- constraint enforcement,
- stopping tests,
- shot allocation,
- measurement grouping,
- error-mitigation postprocessing.

The classical part can therefore dominate total runtime even when the quantum circuit itself is shallow.

## 6. Variational principle

Let $H$ be Hermitian with eigenstates $|E_j\rangle$ and ordered eigenvalues

```math
E_0\le E_1\le E_2\le\cdots.
```

Write an arbitrary normalized state as

```math
|\psi\rangle
=
\sum_j c_j|E_j\rangle,
```

with

```math
\sum_j|c_j|^2=1.
```

Then

```math
\langle\psi|H|\psi\rangle
=
\sum_j|c_j|^2E_j.
```

Since every $E_j\ge E_0$,

```math
\langle\psi|H|\psi\rangle
\ge
E_0\sum_j|c_j|^2
=E_0.
```

Therefore

```math
\boxed{
\langle\psi|H|\psi\rangle\ge E_0
}
```

for every normalized trial state.

## 7. Variational optimization over an ansatz

If the trial state comes from an ansatz,

```math
|\psi(\boldsymbol\theta)\rangle,
```

then

```math
E_{\mathrm{var}}
=
\min_{\boldsymbol\theta}
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle
\ge E_0.
```

This gives an upper bound to the exact ground-state energy.

Equality occurs only if the ansatz can reach a ground state and the optimization finds it exactly.

## 8. Representation error

Suppose the best state inside the ansatz has energy

```math
E_{\mathcal A}
=
\min_{\boldsymbol\theta}
E(\boldsymbol\theta).
```

Then the ansatz or representation error is

```math
\Delta_{\mathrm{ansatz}}
=
E_{\mathcal A}-E_0.
```

No optimizer can reduce this error below zero because the missing solution is outside the hypothesis family.

## 9. Optimization error

Suppose the optimizer returns parameters $\boldsymbol\theta_*$ that are not globally optimal. Then

```math
\Delta_{\mathrm{opt}}
=
E(\boldsymbol\theta_*)-E_{\mathcal A}.
```

This error can come from:

- local minima,
- flat regions,
- noisy gradients,
- poor initialization,
- premature stopping,
- limited optimization budget.

## 10. Sampling error

A quantum expectation value is normally estimated from finite shots.

For a Pauli observable with outcomes $\pm1$, the empirical estimator has variance

```math
\mathrm{Var}(\widehat P)
=
\frac{1-\langle P\rangle^2}{N}
```

for $N$ independent shots.

Thus statistical error decreases only as

```math
O(N^{-1/2}).
```

Reducing measurement uncertainty by a factor of 10 typically requires roughly 100 times more shots in simple sampling.

## 11. Hardware error

Real devices introduce noise:

```math
\rho
\mapsto
\mathcal E(\rho).
```

This can bias the measured objective:

```math
\mathbb E[\widehat C]
\neq
C_{\mathrm{ideal}}.
```

Unlike pure sampling noise, systematic device bias does not disappear merely by taking more shots.

Error mitigation can reduce bias but usually increases sampling or calibration cost.

## 12. Total error decomposition

A useful conceptual decomposition is

```math
\Delta_{\mathrm{total}}
\approx
\Delta_{\mathrm{ansatz}}
+
\Delta_{\mathrm{opt}}
+
\Delta_{\mathrm{sampling}}
+
\Delta_{\mathrm{hardware}}.
```

The terms are not always mathematically independent, but the decomposition is diagnostically useful.

For example, noise can alter the optimization trajectory, and finite-shot gradients can change where the optimizer converges.

## 13. Total computational cost

The cost of a VQA is not simply the depth of one circuit.

A more realistic model is

```math
C_{\mathrm{train}}
\sim
N_{\mathrm{iter}}
\times
N_{\mathrm{settings/iter}}
\times
N_{\mathrm{shots/setting}}
\times
C_{\mathrm{circuit}}.
```

Additional classical postprocessing and communication latency can also matter.

This multiplicative structure is one reason shallow circuits can still lead to expensive algorithms.

## 14. Stopping criteria

Possible stopping rules include:

- small change in cost,
- small gradient norm,
- fixed iteration budget,
- target physical accuracy,
- validation-set performance in QML,
- lack of statistically significant improvement.

On noisy hardware, a tiny observed cost change may be smaller than estimator uncertainty and therefore meaningless.

A statistically aware stopping rule should compare progress against the noise floor.

## 15. Initialization

Initialization can strongly influence trainability.

Random initialization may explore a broad parameter region, but in deep expressive circuits it can place the model inside a concentration regime.

Alternatives include:

- identity-like initialization,
- problem-informed initialization,
- parameter transfer from smaller systems,
- layerwise growth,
- warm starts from classical solutions.

Initialization is therefore part of the algorithm, not an irrelevant implementation detail.

## 16. Worked example: one-qubit variational energy

Take

```math
H=Z
```

and ansatz

```math
|\psi(\theta)\rangle
=
R_y(\theta)|0\rangle.
```

Since

```math
R_y(\theta)|0\rangle
=
\cos\frac\theta2|0\rangle
+
\sin\frac\theta2|1\rangle,
```

we obtain

```math
E(\theta)
=
\langle Z\rangle
=
\cos\theta.
```

The minimum is

```math
E_{\min}=-1
```

at

```math
\theta=\pi\pmod{2\pi}.
```

The ansatz contains the exact ground state $|1\rangle$, so the representation error is zero.

If an optimizer stops at $\theta=0.9\pi$, the remaining error is optimization error, not ansatz error.

## 17. VQA is broader than the variational principle

Not every VQA uses a ground-state variational bound.

A generic VQA may optimize:

- classification loss,
- expectation values,
- overlap objectives,
- combinatorial cost functions,
- fidelity,
- control objectives,
- generative likelihood surrogates.

Thus

```math
\text{VQA}
\supset
\text{variational-eigenvalue algorithms}.
```

The Rayleigh–Ritz variational principle is central to VQE but not the definition of VQA itself.

## 18. Common misconceptions

### “A shallow quantum circuit means a cheap VQA.”

No. Many repeated circuit executions may be required across iterations, parameters, observables, and shots.

### “If VQE returns an energy above the exact value, the optimizer must have failed.”

Not necessarily. The ansatz may exclude the ground state.

### “Taking more shots removes all hardware error.”

No. More shots reduce statistical uncertainty, not systematic bias.

### “The classical optimizer is secondary.”

No. The hybrid optimization loop is part of the algorithm and can dominate total cost.

## 19. Connections

This chapter provides the framework used by:

- VQE,
- QAOA,
- variational quantum simulation,
- trainable QML circuits,
- gradient methods,
- and barren-plateau analysis.

The central diagnostic question is:

> Is failure caused by representation, optimization, measurement, or hardware?

## 20. Exercises

### Conceptual

1. Why does the variational principle provide an upper bound to the ground energy?
2. Explain the difference between ansatz error and optimization error.
3. Why can a shallow circuit still lead to a large total training cost?
4. Why does increasing shot count not remove systematic hardware bias?

### Computational

5. Derive the one-qubit cost $E(\theta)=\cos\theta$ for the worked example.
6. If a Pauli expectation is $\langle P\rangle=0.6$, compute the variance of its $N$-shot empirical estimator.
7. How many more shots are needed to reduce standard error by a factor of 5?
8. Suppose an ansatz minimum is $E_{\mathcal A}=-0.95$ while the exact ground energy is $-1$. If optimization returns $-0.90$, identify the ansatz and optimization errors.

### Research-oriented

9. A VQA paper reports circuit depth but not number of cost evaluations. Why is the resource comparison incomplete?
10. Design an experiment that distinguishes poor ansatz expressivity from optimizer failure.
11. How would you define a statistically meaningful stopping rule when cost estimates have finite-shot uncertainty?
12. In QML, which parts of the error decomposition correspond most closely to approximation error, optimization error, finite-sample error, and hardware error?

## 21. Key takeaways

- A VQA is a hybrid optimization framework using quantum evaluations and classical updates.
- The variational principle gives an upper bound for ground-state energy and underlies VQE.
- Representation, optimization, sampling, and hardware errors are distinct failure modes.
- The cost of a VQA is multiplicative across iterations, circuit settings, shots, and execution cost.
- Initialization, stopping criteria, and classical optimization are genuine algorithmic choices.
- “Shallow circuit” does not imply “cheap algorithm.”

## References

1. M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
2. J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New Journal of Physics* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
3. A. Peruzzo et al., "A variational eigenvalue solver on a photonic quantum processor," *Nature Communications* 5, 4213 (2014). https://doi.org/10.1038/ncomms5213
