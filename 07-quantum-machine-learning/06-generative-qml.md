# Quantum Generative Models

## 1. What generative learning changes

A discriminative model learns a map such as

```math
x\longmapsto y.
```

A generative model instead learns a probability distribution, quantum state, or data-generating process.

Quantum systems naturally generate probability distributions through measurement, so they provide a direct language for generative modeling.

However, **easy quantum sampling is not the same as easy quantum training**.

## 2. Learning objectives

After this chapter, you should be able to:

- define a quantum Born machine,
- distinguish explicit likelihood models from implicit samplers,
- explain likelihood, KL, MMD, adversarial, and moment-matching objectives conceptually,
- identify when probability evaluation is harder than sampling,
- distinguish classical-data generation from quantum-state generation,
- formulate quantum GAN roles precisely,
- analyze mode collapse and trainability issues,
- and evaluate sampling advantage separately from training advantage.

## 3. Born distributions

Let

```math
|\psi_\theta\rangle
=
\sum_x
\psi_\theta(x)|x\rangle.
```

Computational-basis measurement produces the distribution

```math
p_\theta(x)
=
|\psi_\theta(x)|^2.
```

A model using this rule as its generative distribution is often called a **quantum Born machine**.

The trainable state may be prepared by a PQC, analog quantum dynamics, a tensor-network-like circuit, or another quantum process.

## 4. Generative task

Given samples

```math
x_1,\ldots,x_m
\sim
p_{\mathrm{data}},
```

the objective is to choose $\theta$ such that

```math
p_\theta
\approx
p_{\mathrm{data}}.
```

The meaning of “approximately” depends on the training objective and evaluation metric.

Different distances emphasize different failure modes.

## 5. Maximum likelihood

The negative log-likelihood is

```math
\mathcal L_{\mathrm{NLL}}(\theta)
=
-\frac1m
\sum_{i=1}^{m}
\log p_\theta(x_i).
```

Minimizing it is equivalent, in the population limit, to minimizing a KL divergence up to a constant independent of the model.

But this objective requires evaluating

```math
p_\theta(x_i)
```

for training samples.

A quantum device may sample from $p_\theta$ efficiently while exact probability evaluation remains difficult.

## 6. Sampling versus probability evaluation

A quantum circuit can generate a bit string in one execution:

```text
prepare state
-> measure
-> sample x.
```

Estimating one small probability $p_\theta(x)$ to high relative accuracy can require many repetitions.

Thus

```math
\text{efficient sampling}
\not\Rightarrow
\text{efficient likelihood evaluation}.
```

This distinction strongly influences which generative losses are practical.

## 7. KL divergence

For distributions $p$ and $q$,

```math
D_{\mathrm{KL}}(p\|q)
=
\sum_x
p(x)
\log\frac{p(x)}{q(x)}.
```

Different KL directions penalize different errors.

For example,

```math
D_{\mathrm{KL}}(p_{\mathrm{data}}\|p_\theta)
```

strongly penalizes assigning tiny probability to observed data modes.

Direct KL estimation can be difficult when the support is large or model probabilities are not directly accessible.

## 8. Maximum Mean Discrepancy

MMD compares distributions through a classical kernel $k$:

```math
\mathrm{MMD}^2(p,q)
=
\mathbb E_{x,x'\sim p}k(x,x')
+
\mathbb E_{y,y'\sim q}k(y,y')
-
2\mathbb E_{x\sim p,y\sim q}k(x,y).
```

It can be estimated from samples without evaluating full probability tables.

This makes MMD attractive for implicit quantum generators.

But performance depends on kernel choice and sample count.

## 9. Moment matching

Instead of fitting the entire distribution directly, a model can match selected observables or moments:

```math
\mathbb E_{p_\theta}[f_j(X)]
\approx
\mathbb E_{p_{\mathrm{data}}}[f_j(X)].
```

This reduces measurement burden when only certain statistics matter.

The tradeoff is that matching a finite set of moments may not uniquely identify the target distribution.

## 10. Adversarial learning

A generative adversarial model trains a generator against a discriminator.

The generator seeks to produce samples the discriminator cannot distinguish from real data.

A quantum generative adversarial setup can place quantum components in several locations:

```text
quantum generator + classical discriminator
classical generator + quantum discriminator
quantum generator + quantum discriminator
quantum-state data + quantum discriminator.
```

Therefore the acronym **QGAN** is incomplete until the architecture is specified.

## 11. Quantum generator, classical data

Suppose a PQC prepares

```math
|\psi_\theta\rangle
```

and measurements produce classical samples $x$.

A classical discriminator receives either

```text
real classical x
```

or

```text
quantum-generated classical x.
```

In this setting the quantum component is essentially a learnable sampling device.

The central question is whether its sample family or resource scaling is useful relative to strong classical generative models.

## 12. Quantum discriminator

If the data themselves are quantum states, a quantum discriminator can implement a measurement designed to distinguish

```math
\rho_{\mathrm{real}}
```

from

```math
\rho_{\mathrm{gen}}.
```

This setting is more intrinsically quantum because classicalizing the states before discrimination may lose information.

The discriminator can be understood as a trainable POVM or channel-plus-measurement model.

## 13. Generating quantum states

A quantum generator may aim to prepare a target state

```math
\rho_*.
```

The task becomes

```math
\mathcal E_\theta(\rho_0)
\approx
\rho_*.
```

Possible losses include:

- fidelity,
- local observable discrepancies,
- adversarial distinguishability,
- relative-entropy-like quantities,
- physically relevant correlation functions.

This can avoid requiring a full classical description of $\rho_*$ when training data come directly from quantum experiments.

## 14. Many-body state generation

For many-body physics, a generator may learn a family

```math
|\psi(\lambda)\rangle
```

parameterized by physical conditions $\lambda$.

Useful inductive bias can include:

- locality,
- symmetry,
- particle number,
- tensor-network structure,
- known Hamiltonian terms.

A generic random PQC is rarely the only reasonable baseline.

## 15. Mode collapse

A generator can produce only a small subset of target modes while still fooling an imperfect objective or discriminator.

This is mode collapse.

For example, a target distribution may have several well-separated clusters while

```math
p_\theta
```

places nearly all probability on one cluster.

Generative evaluation should therefore examine coverage as well as sample quality.

## 16. Expressibility and trainability

A highly expressive quantum generator can represent complex distributions, but training can become difficult because of:

- barren plateaus,
- noisy probability estimates,
- discriminator instability,
- vanishing gradients,
- support mismatch,
- finite-shot objectives.

As elsewhere in QML,

```math
\text{representation power}
\not\Rightarrow
\text{learnability}.
```

## 17. Gradient estimation

If the generator uses a PQC and the loss is differentiable through expectation values, parameter-shift methods may apply.

But sample-based losses such as empirical MMD can introduce additional stochasticity from both:

```text
finite quantum samples
and
finite training data.
```

Training variance therefore has multiple sources.

## 18. Evaluating generative quality

Useful metrics can include:

- held-out log-likelihood when available,
- MMD,
- total variation distance on tractable small problems,
- Wasserstein-style distances,
- precision/recall-like mode metrics,
- task-specific observable errors,
- downstream utility of generated samples.

No single metric captures every aspect of generative performance.

## 19. Sampling hardness

Some quantum circuits generate distributions believed or known under complexity assumptions to be hard for classical computers to sample exactly or approximately in specified regimes.

But generative learning asks a stronger question:

> Can the model efficiently learn a useful target distribution and then exploit a sampling capability unavailable classically?

A hard random quantum distribution may have no relevance to real data.

Thus

```math
\text{sampling hardness}
\not\Rightarrow
\text{generative learning advantage}.
```

## 20. Training hardness

A distribution can be easy for a quantum device to sample after parameters are known but hard to train from data.

Training may require:

- estimating tiny probability differences,
- resolving noisy gradients,
- many circuit executions,
- expensive classical optimization.

Therefore a complete generative advantage claim needs both efficient **learning** and useful **sampling/inference**.

## 21. Classical baselines

Relevant classical generative baselines include:

- autoregressive models,
- normalizing flows,
- variational autoencoders,
- GANs,
- diffusion models,
- tensor-network Born machines,
- energy-based models,
- problem-specific probabilistic models.

For quantum-state targets, classical tensor networks and neural quantum states may be particularly important.

## 22. Quantum Born machine versus classical Born machine

Tensor-network or neural wavefunction models can also define probabilities through squared amplitudes.

Thus the Born-rule form

```math
p(x)=|\psi(x)|^2
```

is not by itself a certificate of quantum advantage.

The comparison should ask whether the quantum state family can be represented, trained, and sampled more efficiently than relevant classical amplitude models.

## 23. Generative model as a channel

The generator need not output only computational-basis samples.

A general generator is a parameterized channel

```math
\mathcal G_\theta:
\rho_0
\mapsto
\rho_\theta.
```

This allows:

- dissipative state generation,
- mixed-state modeling,
- noise-aware generation,
- conditional quantum generation.

The channel viewpoint is especially natural when the target is itself mixed or noisy.

## 24. Conditional generation

A conditional generator receives context $c$:

```math
\rho_{\theta,c}
=
\mathcal G_\theta(c).
```

The context can be encoded classically or quantum mechanically.

Applications might include generating a quantum state at a requested physical parameter, graph condition, or measurement setting.

This connects generative QML to surrogate modeling of quantum experiments.

## 25. Resource accounting

A generative-QML resource analysis should include:

```text
state/data encoding
quantum samples per loss estimate
number of discriminator updates
number of generator updates
gradient circuit settings
shots per setting
inference samples required
classical postprocessing
```

For quantum-state generation, also count copies of target states or experiments consumed during training.

## 26. Advantage taxonomy

Generative quantum advantage can mean several different things.

### Sampling advantage

The trained quantum model samples from a useful distribution more efficiently.

### Representation advantage

The target distribution/state has a compact quantum representation relative to a restricted classical class.

### Training-data advantage

The quantum learner needs fewer copies/experiments to learn a quantum target.

### Runtime advantage

The complete training-plus-generation pipeline is faster under comparable resources.

These claims should not be conflated.

## 27. Common misconceptions

### “If a quantum circuit is hard to sample classically, it is a good generative model.”

No. Hardness and target usefulness are different properties.

### “Sampling from a Born machine gives its likelihood for free.”

No. Probability evaluation can be much harder than sample generation.

### “QGAN defines one architecture.”

No. Generator, discriminator, and data can each be classical or quantum in different constructions.

### “Quantum generative advantage follows from output entropy or entanglement.”

No. One must establish useful target fit and resource separation.

## 28. Worked example: two-bit target distribution

Suppose the target is

```math
p_{\mathrm{data}}(00)=\frac12,
\qquad
p_{\mathrm{data}}(11)=\frac12,
```

with zero probability on $01$ and $10$.

The Bell state

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2}
```

reproduces this classical measurement distribution exactly.

But the separable mixed state

```math
\rho
=
\frac12|00\rangle\langle00|
+
\frac12|11\rangle\langle11|
```

produces the **same** classical distribution.

Therefore entanglement is not necessary for this generative task if only computational-basis samples matter.

This is a useful resource-ablation lesson.

## 29. Research direction: quantum-native generative targets

To make genuinely quantum structure necessary, define a target that includes incompatible observables or coherent state properties rather than one fixed classical measurement distribution.

For example, require the generator to reproduce statistics across several noncommuting measurements.

Then the target becomes a quantum state/process rather than a classical histogram.

This is a more natural setting for testing genuinely quantum generative resources.

## 30. Exercises

### Conceptual

1. Distinguish generative sampling from likelihood evaluation.
2. Why does hard-to-sample output not prove learning advantage?
3. Why can a separable mixed state reproduce the same classical samples as an entangled Bell state in the worked example?
4. What changes when the target is a quantum state rather than one measurement distribution?

### Computational

5. Compute the Born probabilities of

```math
|\psi(\theta)\rangle
=
\cos\theta|00\rangle+
\sin\theta|11\rangle.
```
6. Find $\theta$ that reproduces the balanced $00/11$ target distribution.
7. Write the empirical MMD estimator conceptually for $m$ real and $m$ generated samples.
8. Suppose each generator-loss estimate uses 2000 quantum samples and training uses 5000 updates. Estimate the raw generated-sample count.

### Research-oriented

9. Design a resource-destroying ablation to test whether coherence is necessary for a quantum generative task.
10. Compare a quantum Born machine with a tensor-network Born machine under matched parameter count and sampling budget.
11. Formulate a quantum-native generative benchmark requiring reproduction of noncommuting measurement statistics.
12. What evidence would distinguish sampling advantage from trainability advantage?

## 31. Key takeaways

- Quantum generative models learn distributions, states, or processes rather than only label functions.
- Born machines convert quantum amplitudes into samples through measurement.
- Efficient sampling does not imply efficient probability evaluation or training.
- QGAN is an umbrella term whose quantum components must be specified.
- Sampling hardness is not enough; the learned target must be useful and trainable.
- Quantum-state generation is more intrinsically quantum than matching one classical measurement histogram.
- Fair evaluation requires strong classical generative baselines and complete training-resource accounting.

## References

1. S. Lloyd and C. Weedbrook, "Quantum generative adversarial learning," *Physical Review Letters* 121, 040502 (2018). https://doi.org/10.1103/PhysRevLett.121.040502
2. M. Benedetti et al., "A generative modeling approach for benchmarking and training shallow quantum circuits," *npj Quantum Information* 5, 45 (2019). https://doi.org/10.1038/s41534-019-0157-8
3. J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
