# Trainability in Quantum Machine Learning

## 1. Trainability is broader than barren plateaus

A QML model is trainable when useful information about improving the learning objective can be extracted with scalable computational and measurement resources.

Barren plateaus are one important failure mode, but trainability also depends on:

- data encoding,
- cost design,
- circuit architecture,
- initialization,
- measurement noise,
- dataset averaging,
- optimizer information,
- hardware noise,
- parameter identifiability.

The operational question is

```math
\boxed{
\text{Can the learner resolve a useful update direction
with affordable resources?}
}
```

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish ideal gradient magnitude from measurable optimization signal,
- explain architecture-induced and data-induced concentration,
- connect quantum-kernel concentration with variational trainability,
- distinguish finite-shot noise from hardware bias,
- analyze how minibatching and dataset averaging affect gradient variance,
- identify initialization and locality as trainability controls,
- distinguish flatness from redundancy and poor conditioning,
- formulate operational signal-to-noise trainability metrics,
- and design scaling experiments that diagnose the mechanism of failure.

## 3. Supervised QML objective

Consider empirical risk

```math
\widehat{\mathcal L}(\theta)
=
\frac1m
\sum_{i=1}^{m}
\ell
\left(
f_\theta(x_i),y_i
\right).
```

A parameter gradient is

```math
\frac{\partial\widehat{\mathcal L}}{\partial\theta_j}
=
\frac1m
\sum_i
\frac{\partial\ell_i}{\partial f_i}
\frac{\partial f_\theta(x_i)}{\partial\theta_j}.
```

Trainability therefore depends jointly on:

```text
loss sensitivity
x model-output sensitivity
x dataset averaging.
```

A circuit can have nonzero output gradients on individual examples while the full-dataset gradient cancels.

## 4. Ideal barren plateaus

For some random/expressive circuit families,

```math
\mathbb E
\left[
\partial_{\theta_j}\mathcal L
\right]
\approx0
```

and

```math
\mathrm{Var}
\left[
\partial_{\theta_j}\mathcal L
\right]
\sim
e^{-cn}.
```

Typical gradient magnitude then becomes exponentially small in qubit number $n$.

If the estimator noise decreases only as $N^{-1/2}$ with shots, resolving such gradients can require exponentially many measurements.

## 5. Operational signal-to-noise ratio

Let $\widehat g_j$ be a measured gradient estimator.

Define

```math
\mathrm{SNR}_j
=
\frac{
|\mathbb E[\widehat g_j]|
}{
\sqrt{\mathrm{Var}(\widehat g_j)}
}.
```

A mathematically nonzero gradient is not practically useful when

```math
\mathrm{SNR}_j\ll1.
```

This makes trainability explicitly budget dependent.

A model can be trainable at $10^9$ shots per step but untrainable at $10^4$ shots per step.

## 6. Data-induced concentration

Even a circuit architecture that avoids random-circuit barren plateaus can lose sensitivity because of its data embedding.

Suppose encoded states satisfy

```math
\rho(x)
\approx
\rho(x')
```

for most data points, or observable values concentrate around a common value.

Then predictions become insensitive to example identity.

Alternatively, embeddings may become almost mutually orthogonal and destroy smooth target-relevant geometry.

Thus data distribution and feature map can create concentration independently of trainable-circuit randomness.

## 7. Dataset-induced cancellation

Suppose per-example gradients are

```math
g_i
=
\nabla_\theta\ell_i.
```

The full-batch gradient is

```math
\bar g
=
\frac1m\sum_i g_i.
```

Large $\|g_i\|$ does not guarantee large $\|\bar g\|$.

If gradients point in inconsistent directions across examples, averaging can produce cancellation.

This is a learning-specific effect beyond single-cost barren-plateau analysis.

## 8. Minibatching

A minibatch $B$ gives estimator

```math
\widehat g_B
=
\frac1{|B|}
\sum_{i\in B}g_i.
```

Small batches increase stochastic variance but may preserve directional signals hidden by exact full-batch cancellation.

Large batches reduce data-sampling noise but can be expensive on quantum hardware because each example requires circuit evaluation.

Thus batch size is both a statistical and quantum-execution hyperparameter.

## 9. Two noise sources in a QML gradient

A minibatch gradient can vary because of:

```text
which data points were sampled
```

and

```text
quantum measurement shots.
```

Schematically,

```math
\mathrm{Var}(\widehat g)
=
\mathrm{Var}_{\mathrm{data}}
+
\mathrm{Var}_{\mathrm{shots}}
+
\text{interaction terms}.
```

Optimization design should determine which source dominates before simply increasing shot count.

## 10. Hardware noise

A noisy model implements

```math
\rho_{x,\theta}^{\mathrm{noisy}}
=
\mathcal N
\circ
\mathcal E_{x,\theta}(\rho_0).
```

The measured model is then different from the ideal hypothesis class.

Noise can:

- suppress parameter dependence,
- bias gradients,
- contract state distinguishability,
- alter the optimal parameters.

Taking more shots does not remove this bias.

## 11. Noise-induced gradient suppression

If each layer contracts parameter information by factor

```math
0<\lambda<1,
```

then influence from an early layer can scale schematically as

```math
\lambda^L
```

after depth $L$.

Thus a model can be trainable in simulation and effectively flat on hardware.

Hardware trainability should therefore be benchmarked separately from ideal trainability.

## 12. Global versus local measurements

A global cost can depend on correlations across the whole register.

A local cost

```math
C
=
\frac1n
\sum_i
\langle O_i\rangle
```

has smaller causal support in shallow local circuits.

Locality can preserve stronger gradients because parameters affect limited light cones rather than one global concentrated observable.

But local costs can fail to encode the desired global task fully.

## 13. Readout bottleneck

A highly expressive state

```math
\rho_{x,\theta}
```

can contain information that the chosen measurement cannot access.

If the readout is only

```math
\langle Z_1\rangle,
```

parameters affecting correlations outside the $Z_1$ causal cone may be invisible.

This is not necessarily a barren plateau; it can be an **observability problem**.

The trainable measurement perspective can sometimes address this bottleneck.

## 14. Parameter redundancy

Suppose

```math
f_{\theta_1,\theta_2}(x)
=
f_{\theta_1+\theta_2}(x).
```

Then direction

```math
(1,-1)
```

changes parameters without changing the model.

The corresponding Fisher/Hessian direction is singular or flat.

This is parameter non-identifiability, not concentration over Hilbert space.

Removing redundant parameterization can improve optimizer conditioning.

## 15. Hessian conditioning

Near an optimum, curvature is described by a Hessian

```math
H_{ij}
=
\frac{\partial^2\mathcal L}
{\partial\theta_i\partial\theta_j}.
```

If eigenvalues span many orders of magnitude, optimization can be ill-conditioned:

```text
steep directions
+
very flat directions.
```

A model can avoid exponentially vanishing first derivatives yet still be difficult to optimize because of poor curvature.

## 16. Fisher-information viewpoint

A parameterized probability model

```math
p_\theta(y|x)
```

has Fisher information

```math
F_{ij}
=
\mathbb E
\left[
\partial_i\log p_\theta
\partial_j\log p_\theta
\right].
```

Small eigenvalues indicate parameter directions that weakly affect observable distributions.

This connects trainability with **identifiability** rather than only loss-landscape gradients.

## 17. Initialization

Random initialization is not neutral.

Deep random circuits can begin near concentration regimes.

Alternatives include:

```text
near-identity initialization
small-angle initialization
problem-informed parameters
classical warm starts
layerwise growth
parameter transfer.
```

The goal is to start in a region where model outputs respond detectably to parameter changes.

## 18. Layerwise training

Train a shallow model first:

```text
L=1
-> optimize
-> append layer
-> optimize
-> ...
```

This prevents all layers from starting as a deep random circuit.

The method can improve optimization empirically, but one should test whether it improves scaling or only small-system constants.

## 19. Symmetry-preserving models

If the task obeys symmetry $G$, restricting the model to the correct symmetry sector can reduce irrelevant parameter directions.

For generator $Q$,

```math
[U_\theta,Q]=0
```

keeps states inside fixed sectors.

This can simultaneously improve:

- representation efficiency,
- generalization,
- trainability.

But an incorrect symmetry assumption can make the target unreachable.

## 20. Architecture and light cones

Local circuits create finite causal cones.

If data feature $x_j$ is encoded far from measured observable $M$ and depth is too shallow to connect them, then

```math
\frac{\partial f}{\partial x_j}=0.
```

Similarly, distant trainable parameters may have zero influence.

This is an architecture-induced dead feature, not statistical concentration.

A causal-cone audit can diagnose it exactly.

## 21. Quantum-kernel concentration as trainability analogue

Fixed quantum kernels have no trainable circuit parameters, but kernel values can concentrate exponentially:

```math
K(x,x')
\approx c.
```

Then informative differences require high measurement precision.

This is conceptually parallel to a barren plateau:

```text
variational model:
parameter derivative becomes tiny

kernel model:
pairwise similarity difference becomes tiny.
```

Both are examples of **information concentration making learning signals inaccessible**.

## 22. A unified information-flow view

Many trainability failures can be expressed as loss of distinguishability.

A parameter update, data change, or class difference should induce a measurable change in the output distribution.

If

```math
p_{\theta}(y|x)
\approx
p_{\theta+\delta}(y|x)
```

for all accessible measurements, the optimizer receives little information about $\delta$.

Similarly, if

```math
p_\theta(y|x)
\approx
p_\theta(y|x')
```

for different examples, the model cannot distinguish them effectively.

This suggests trainability as an information-transmission problem through the QML pipeline.

## 23. Input-gradient trainability

One can study sensitivity to data as well as parameters:

```math
\frac{\partial f_\theta(x)}{\partial x_j}.
```

If data gradients vanish, the model may fail to resolve input differences even when parameter gradients are nonzero.

This is especially relevant for robustness, adversarial sensitivity, and feature-map concentration.

## 24. Trainability versus expressivity

A model can be:

```text
low expressivity + trainable
high expressivity + trainable
low expressivity + untrainable
high expressivity + untrainable.
```

These are separate axes.

Research should not use expressibility metrics as proxies for trainability without direct evidence.

## 25. Trainability versus generalization

An easily optimized model may overfit.

A restricted model may generalize well but be difficult to train because of a poor parameterization.

Thus the desired region is not simply “largest gradients.”

One seeks

```text
sufficient representation
+ resolvable optimization signal
+ good statistical inductive bias.
```

## 26. Optimizer choice

Gradient descent, SPSA, natural gradient, evolutionary methods, and derivative-free optimizers consume different information.

Changing optimizer can improve robustness to noisy gradients or conditioning.

But if all local model differences are below the measurement noise floor, no optimizer can recover information that was never measured.

This is an information-theoretic limit on optimization.

## 27. Adaptive shot allocation

Instead of using fixed shots for every gradient component, allocate measurement budget to uncertain or important directions.

For example, estimate a gradient coarsely first and increase shots only when its sign is ambiguous.

This can reduce average training cost when many gradients are large enough to resolve cheaply.

Adaptive measurement is therefore an optimization resource.

## 28. Training cost metric

A useful operational metric is

```math
N_{\mathrm{shots\ to\ target}}
```

or total circuit executions required to reach specified validation performance.

This includes the fact that one architecture may have larger per-step gradients but require many more parameters or iterations.

Comparing only gradient variance can miss this total cost.

## 29. Scaling experiment

To diagnose trainability:

1. choose system sizes $n$;
2. choose fixed architecture scaling rules;
3. sample multiple datasets/initializations;
4. estimate gradient distributions;
5. record shot budget needed for fixed SNR;
6. train under matched budgets;
7. compare validation performance and time-to-target.

This is stronger than showing one optimizer trace at one $n$.

## 30. Mechanism ablations

A good trainability study can ablate:

```text
depth
initialization
entangling topology
cost locality
data encoding
noise
dataset size
measurement choice.
```

If only one variable changes at a time, the mechanism becomes interpretable.

## 31. Edge-of-concentration hypothesis

A speculative research direction is that useful models may live near a transition:

```text
underexpressive / strongly structured
<->
rich but trainable
<->
overconcentrated / random-like.
```

One could define order parameters such as:

```math
\mathrm{Var}(\partial_\theta\mathcal L),
```

entanglement growth, or Fisher-spectrum statistics and test whether learning performance peaks near a transition region.

This is a hypothesis, not an established universal law.

## 32. Common misconceptions

### “Barren plateaus are the only QML trainability problem.”

No. Data concentration, cancellation, readout blindness, redundancy, noise, and conditioning can all matter.

### “A nonzero analytic gradient means the model is trainable.”

Not if measurement resources cannot resolve it.

### “More shots always solve optimization.”

Not hardware bias or structural zero-gradient directions.

### “Kernel models avoid trainability problems.”

They avoid parameter-gradient optimization but can suffer kernel concentration and measurement precision issues.

### “Changing optimizer fixes an information-poor model.”

No optimizer can use information absent from accessible measurements.

## 33. Trainability audit template

Record:

```text
system size scaling:
circuit depth scaling:
data encoding:
cost/readout locality:
initialization distribution:
per-example gradient statistics:
full-batch gradient statistics:
shot noise:
hardware bias:
Fisher/Hessian conditioning:
training shots to target:
validation performance:
```

This helps separate ideal landscape geometry from operational trainability.

## 34. Exercises

### Conceptual

1. Why can per-example gradients be large while the full-batch gradient is small?
2. Distinguish a barren plateau from a zero gradient caused by a disconnected light cone.
3. Why are quantum-kernel concentration and variational barren plateaus conceptually related?
4. Explain why Fisher-information eigenvalues are relevant to trainability.

### Computational

5. If a typical gradient scales as $2^{-n/2}$ and shot noise as $N^{-1/2}$, derive the shot scaling for constant SNR.
6. Suppose $m$ independent per-example gradients have zero mean and variance $\sigma^2$. Compute the variance of their average.
7. If a noise channel contracts sensitivity by $0.95$ per layer, estimate the remaining fraction after 100 layers.
8. For a two-parameter model depending only on $\theta_1+\theta_2$, identify one redundant direction.

### Research-oriented

9. Design an experiment separating data-induced concentration from architecture-induced concentration.
10. Define an operational trainability metric based on total quantum shots to reach a validation threshold.
11. Test the edge-of-concentration hypothesis using gradient variance and generalization as system size grows.
12. Can a trainable measurement recover learning signal lost by a fixed readout? Design a toy experiment.

## 35. Key takeaways

- QML trainability means useful optimization information is measurable with scalable resources.
- Barren plateaus are only one mechanism of signal loss.
- Data encoding, dataset averaging, readout choice, noise, redundancy, and conditioning can independently suppress useful gradients.
- Operational SNR and shots-to-target are often more meaningful than ideal gradient magnitude alone.
- Quantum kernels can suffer an analogous concentration problem even without trainable parameters.
- Trainability, expressivity, and generalization should be measured separately.
- Mechanism-specific scaling studies are stronger than small-system optimizer demonstrations.

## References

1. J. R. McClean et al., "Barren plateaus in quantum neural network training landscapes," *Nature Communications* 9, 4812 (2018). https://doi.org/10.1038/s41467-018-07090-4
2. M. Cerezo et al., "Cost function dependent barren plateaus in shallow parametrized quantum circuits," *Nature Communications* 12, 1791 (2021). https://doi.org/10.1038/s41467-021-21728-w
3. S. Wang et al., "Noise-induced barren plateaus in variational quantum algorithms," *Nature Communications* 12, 6961 (2021). https://doi.org/10.1038/s41467-021-27045-6
4. S. Thanasilp et al., "Exponential concentration and untrainability in quantum kernel methods." https://arxiv.org/abs/2208.11060
