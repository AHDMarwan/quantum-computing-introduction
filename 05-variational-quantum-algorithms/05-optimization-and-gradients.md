# Optimization, Gradients, and Measurement Cost

## 1. The objective is stochastic

A variational cost evaluated on hardware is typically estimated from finite shots. If

```math
C(\boldsymbol\theta)=\langle O\rangle_{\boldsymbol\theta},
```

hardware returns an estimator

```math
\widehat C(\boldsymbol\theta)
=C(\boldsymbol\theta)+\text{sampling noise}+\text{device error}.
```

Optimization therefore occurs with noisy function information.

## 2. Parameter-shift rule

For a gate

```math
U(\theta)=e^{-i\theta G}
```

with a generator having an appropriate two-eigenvalue spectrum, derivatives can often be evaluated exactly through shifted circuit expectations. In the common Pauli-rotation convention,

```math
\frac{\partial C}{\partial\theta}
=
\frac12
\left[
C\!\left(\theta+\frac\pi2\right)
-
C\!\left(\theta-\frac\pi2\right)
\right].
```

This is not finite differencing: under the stated generator conditions it is an analytic identity.

## 3. Gradient cost

If a model has $P$ parameters, naively evaluating all parameter-shift gradients may require $O(P)$ circuit settings per optimization step, multiplied by the shots needed for acceptable statistical precision.

The relevant training cost is therefore closer to

```math
\text{iterations}
\times
\text{circuit settings per iteration}
\times
\text{shots per setting}
\times
\text{circuit execution cost}.
```

## 4. Optimizer families

Common strategies include

- gradient descent and adaptive first-order methods,
- stochastic approximation such as SPSA,
- quasi-Newton methods,
- natural-gradient or quantum-natural-gradient methods,
- and derivative-free optimizers.

No optimizer removes a fundamentally uninformative landscape.

## 5. Geometry

Parameterized quantum states define a geometry related to the quantum Fisher information or Fubini–Study metric. Natural-gradient methods rescale parameter updates using this geometry rather than treating parameter coordinates as Euclidean.

## 6. Measurement allocation

For costs expressed as sums of observables,

```math
C=\sum_j c_j\langle P_j\rangle,
```

shots can be allocated nonuniformly to reduce estimator variance. Measurement grouping and classical-shadow-style protocols can reduce cost in suitable observable regimes.

## 7. Noise and bias

Sampling noise is statistical and decreases with shots. Hardware noise can introduce systematic bias that does not vanish by repeated sampling. Error mitigation may reduce bias but adds its own sampling or calibration overhead.

## References

1. K. Mitarai et al., "Quantum circuit learning," *Phys. Rev. A* 98, 032309 (2018). https://doi.org/10.1103/PhysRevA.98.032309
2. M. Schuld et al., "Evaluating analytic gradients on quantum hardware," *Phys. Rev. A* 99, 032331 (2019). https://doi.org/10.1103/PhysRevA.99.032331
3. J. Stokes et al., "Quantum Natural Gradient," *Quantum* 4, 269 (2020). https://doi.org/10.22331/q-2020-05-25-269
