# Optimization, Gradients, and Measurement Cost

## 1. Why optimization is a first-class quantum resource question

Variational algorithms do not evaluate exact deterministic objectives. On hardware, a cost such as

```math
C(\boldsymbol\theta)
=
\langle O\rangle_{\boldsymbol\theta}
```

is estimated statistically:

```math
\widehat C(\boldsymbol\theta)
=
C(\boldsymbol\theta)
+
\text{sampling fluctuation}
+
\text{hardware bias}.
```

Optimization therefore occurs in a noisy information environment.

The total training burden depends jointly on:

```text
number of parameters
x objective/gradient circuit settings
x shots per setting
x optimization iterations
x circuit execution cost.
```

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish exact costs from finite-shot estimators,
- derive the parameter-shift rule for a Pauli-generated rotation,
- explain why parameter-shift is not finite differencing,
- estimate the shot cost of a gradient vector,
- compare gradient-based and gradient-free optimizers,
- explain simultaneous perturbation methods,
- interpret quantum natural gradient geometrically,
- separate sampling variance from hardware bias,
- and formulate realistic VQA training cost.

## 3. Finite-shot objective estimation

Suppose $P$ is a Pauli observable with outcomes $s\in\{-1,+1\}$.

From $N$ shots,

```math
\widehat{\langle P\rangle}
=
\frac1N\sum_{k=1}^{N}s_k.
```

The estimator is unbiased in the ideal sampling model:

```math
\mathbb E[\widehat{\langle P\rangle}]
=
\langle P\rangle.
```

Its variance is

```math
\mathrm{Var}
\left[
\widehat{\langle P\rangle}
\right]
=
\frac{1-\langle P\rangle^2}{N}.
```

Thus standard error scales as

```math
O(N^{-1/2}).
```

## 4. Costs built from many observables

For

```math
C(\boldsymbol\theta)
=
\sum_j c_j
\langle P_j\rangle_{\boldsymbol\theta},
```

and independently measured terms,

```math
\mathrm{Var}(\widehat C)
=
\sum_j
c_j^2
\mathrm{Var}
\left[
\widehat{\langle P_j\rangle}
\right].
```

This immediately suggests nonuniform shot allocation: terms with large coefficients or large variance may deserve more measurements.

Measurement grouping can also change covariance structure and the number of circuit settings.

## 5. Finite differences

A naive numerical derivative is

```math
\frac{\partial C}{\partial\theta}
\approx
\frac{C(\theta+h)-C(\theta-h)}{2h}.
```

This introduces a tradeoff:

- large $h$ creates truncation bias,
- small $h$ amplifies statistical noise after division by $h$.

This motivates analytic quantum gradient identities whenever possible.

## 6. Parameter-shift rule

Consider a gate

```math
U(\theta)
=
e^{-i\theta P/2},
```

where

```math
P^2=I.
```

For an expectation-value cost, the dependence on $\theta$ has sinusoidal form,

```math
C(\theta)
=
a+b\cos\theta+c\sin\theta
```

when the rest of the circuit is fixed.

Then

```math
C\left(\theta+\frac\pi2\right)
-
C\left(\theta-\frac\pi2\right)
=
2\frac{dC}{d\theta}.
```

Therefore

```math
\boxed{
\frac{\partial C}{\partial\theta}
=
\frac12
\left[
C\left(\theta+\frac\pi2\right)
-
C\left(\theta-\frac\pi2\right)
\right]
}
```

for the standard Pauli-rotation convention.

## 7. Why parameter shift is not finite differencing

The shift

```math
\frac\pi2
```

is not chosen to be “small.” The formula is an exact analytic identity under the relevant generator spectrum assumptions.

There is no finite-difference truncation error.

There is still statistical estimation error because each shifted expectation is measured with finite shots.

## 8. Gradient estimator variance

If the two shifted costs are estimated independently with equal shot count, then

```math
\widehat g
=
\frac12
\left(
\widehat C_+
-
\widehat C_-
\right).
```

Its variance is

```math
\mathrm{Var}(\widehat g)
=
\frac14
\left[
\mathrm{Var}(\widehat C_+)
+
\mathrm{Var}(\widehat C_-)
\right].
```

Thus a small true gradient can be difficult to resolve if its magnitude is below the estimator noise floor.

This becomes central in barren-plateau regimes.

## 9. Cost of a full gradient

Suppose the circuit has $P$ parameters and each parameter uses the simple two-shift rule.

A naive full gradient requires approximately

```math
2P
```

shifted objective evaluations per optimization iteration, before counting repeated shots and observable groups.

A rough training cost is

```math
C_{\mathrm{grad\ train}}
\sim
N_{\mathrm{iter}}
\times
2P
\times
N_{\mathrm{groups}}
\times
N_{\mathrm{shots}}
\times
C_{\mathrm{circuit}}.
```

This can dominate the cost even when each circuit is individually shallow.

## 10. Generalized shift rules

The simple two-term rule applies to generators with the appropriate two-eigenvalue structure.

More general generators can require:

- multiple shifted evaluations,
- linear-combination formulas,
- ancilla-assisted differentiation,
- automatic-differentiation decompositions,
- or other analytic constructions.

Therefore “parameter shift costs two circuits per parameter” is not a universal statement.

## 11. Gradient descent

The simplest update is

```math
\boldsymbol\theta_{t+1}
=
\boldsymbol\theta_t
-
\eta_t
\widehat{\nabla C}(\boldsymbol\theta_t).
```

The learning rate $\eta_t$ controls the update scale.

With noisy gradients:

- too small a learning rate can make progress slower than statistical fluctuations,
- too large a learning rate can cause unstable jumps.

Adaptive optimizers modify coordinate-wise step sizes using gradient-history statistics.

## 12. SPSA and simultaneous perturbations

Simultaneous Perturbation Stochastic Approximation (SPSA) estimates a gradient direction from only a small number of objective evaluations per iteration, independent of parameter count at the level of circuit settings.

Choose a random perturbation vector

```math
\boldsymbol\Delta_t
```

and evaluate

```math
C(\boldsymbol\theta_t+c_t\boldsymbol\Delta_t)
```

and

```math
C(\boldsymbol\theta_t-c_t\boldsymbol\Delta_t).
```

The gradient estimate is reconstructed from the directional difference.

This greatly reduces circuit-setting count compared with evaluating every coordinate separately, but the estimator can have higher variance.

It is a tradeoff, not a free reduction.

## 13. Derivative-free methods

Derivative-free optimizers use objective values directly. Examples include simplex methods, evolutionary strategies, trust-region methods, and Bayesian optimization in low-dimensional regimes.

They can be useful when gradients are expensive or unreliable.

But a derivative-free optimizer cannot solve a fundamentally flat or information-poor landscape automatically.

## 14. Geometry of quantum states

Parameter coordinates do not necessarily reflect physical distance between states.

Two large parameter changes can produce nearly the same state, while a small parameter change can significantly alter the state in another region.

For pure states, infinitesimal distinguishability is related to the Fubini–Study metric. In a parameterized model, one obtains a metric matrix $F$ related to quantum Fisher information.

A natural-gradient update takes the schematic form

```math
\Delta\boldsymbol\theta
=
-\eta
F^{-1}
\nabla C.
```

The metric rescales updates according to state-space geometry rather than raw parameter coordinates.

## 15. Quantum natural gradient cost

Natural gradient can improve optimization geometry, but computing or approximating $F$ adds cost.

For $P$ parameters, a full dense metric has

```math
O(P^2)
```

entries.

Practical methods therefore use approximations such as:

- block-diagonal metrics,
- diagonal approximations,
- stochastic estimates,
- regularized inverses.

Thus improved optimization geometry trades against additional measurement and classical linear-algebra cost.

## 16. Shot allocation

Suppose the total shot budget is

```math
N_{\mathrm{tot}}
=
\sum_jN_j.
```

Uniform allocation

```math
N_j=N_{\mathrm{tot}}/M
```

is rarely variance-optimal when terms have different $|c_j|$ and variances.

An adaptive strategy can allocate more shots where the contribution to objective uncertainty is largest.

Shot allocation is therefore part of the optimization algorithm.

## 17. Correlated measurements and grouping

If several compatible observables are estimated from the same samples, their estimators can be correlated.

Then

```math
\mathrm{Var}
\left(
\sum_j c_j\widehat P_j
\right)
```

contains covariance terms.

Grouping reduces circuit settings but can change estimator variance. Optimizing measurement cost requires considering both effects.

## 18. Hardware noise versus sampling noise

Sampling noise is statistical:

```math
\text{standard error}
\propto
N^{-1/2}.
```

Hardware noise can introduce bias:

```math
\mathbb E[\widehat C]
-C_{\mathrm{ideal}}
\neq0.
```

Taking more shots reduces uncertainty around the biased value but does not remove the bias itself.

This distinction is critical when interpreting optimizer convergence.

## 19. Error mitigation

Error-mitigation methods attempt to infer a less biased estimate without full fault tolerance.

They can require:

- additional circuit executions,
- noise scaling,
- calibration circuits,
- quasiprobability sampling,
- symmetry checks.

A mitigated estimate with lower bias can have much larger variance.

Therefore mitigation should be evaluated using total sampling cost, not accuracy alone.

## 20. Worked example: resolving a small gradient

Suppose the true gradient is

```math
g=10^{-3}.
```

If the standard deviation of the gradient estimator is

```math
\sigma_g=10^{-2},
```

then one evaluation gives a signal-to-noise ratio

```math
\frac{|g|}{\sigma_g}=0.1.
```

The optimizer cannot reliably determine the gradient sign.

If averaging independent estimates reduces uncertainty as $1/\sqrt N$, decreasing the standard deviation by a factor of 10 requires about 100 times more sampling effort.

This illustrates why exponentially small gradients can imply exponentially large measurement requirements.

## 21. Common misconceptions

### “Parameter shift is a finite-difference approximation.”

No. Under its generator assumptions, it is exact apart from statistical/hardware estimation error.

### “Gradient computation costs two circuits.”

Usually it costs two shifted settings **per parameter**, and each setting may require many observables and shots.

### “Gradient-free optimization avoids barren plateaus.”

Not generally. If the objective contains exponentially little local information, every optimizer has a difficult inference problem.

### “More shots fix noisy hardware.”

More shots reduce sampling uncertainty, not systematic noise bias.

## 22. Connections to QML

Everything here reappears in variational QML.

Training a VQC with $P$ parameters over $B$ data points can have cost resembling

```math
N_{\mathrm{epochs}}
\times
B
\times
N_{\mathrm{gradient\ settings}}
\times
N_{\mathrm{shots}}
\times
C_{\mathrm{circuit}}.
```

Thus a quantum model with few trainable parameters can still have high training cost if each gradient requires many quantum executions.

## 23. Exercises

### Conceptual

1. Why does finite-shot optimization differ from optimizing an exact classical function?
2. Explain why parameter shift has no small-step truncation error.
3. Why can SPSA reduce circuit-setting count but increase estimator variance?
4. Why does natural gradient depend on model geometry rather than only the loss function?

### Computational

5. Derive the parameter-shift rule starting from $C(\theta)=a+b\cos\theta+c\sin\theta$.
6. If $P=100$, a full parameter-shift gradient uses two settings per parameter, 20 observable groups per setting, and 1000 shots per group, estimate the shot count per gradient step.
7. If the standard error must be reduced by a factor of 20, by what factor must the independent shot count increase?
8. For two correlated estimators $X,Y$, expand $\mathrm{Var}(aX+bY)$ and identify the covariance contribution.

### Research-oriented

9. A QML paper reports only the number of trainable parameters. What additional quantum training resources should be reported?
10. Design a comparison between parameter shift and SPSA that fixes total shot budget rather than number of optimizer iterations.
11. When could the extra cost of quantum natural gradient be justified?
12. How would you experimentally distinguish gradient suppression caused by circuit structure from suppression caused primarily by hardware noise?

## 24. Key takeaways

- VQA objectives and gradients are statistical estimators on quantum hardware.
- Parameter-shift rules can compute exact analytic derivatives under specific generator conditions.
- Full-gradient cost often scales with parameter count, observable groups, shots, and optimization iterations.
- SPSA, natural gradient, and derivative-free methods trade different resources; none removes fundamental landscape limitations.
- Sampling noise and hardware bias are different phenomena.
- Measurement allocation and error mitigation are part of algorithm design, not secondary implementation details.

## References

1. K. Mitarai et al., "Quantum circuit learning," *Physical Review A* 98, 032309 (2018). https://doi.org/10.1103/PhysRevA.98.032309
2. M. Schuld et al., "Evaluating analytic gradients on quantum hardware," *Physical Review A* 99, 032331 (2019). https://doi.org/10.1103/PhysRevA.99.032331
3. J. Stokes et al., "Quantum Natural Gradient," *Quantum* 4, 269 (2020). https://doi.org/10.22331/q-2020-05-25-269
4. M. Cerezo et al., "Variational quantum algorithms," *Nature Reviews Physics* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
