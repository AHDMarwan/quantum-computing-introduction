# Quantum Generative Models

## 1. Generative learning

A generative model aims to learn a probability distribution, quantum state, or data-generating process rather than only a discriminative map \(x\mapsto y\).

Quantum systems naturally produce probability distributions through measurement, making them candidates for generative modeling.

## 2. Born machines

A parameterized state

\[
|\psi(\boldsymbol\theta)\rangle
=
\sum_x \psi_{\boldsymbol\theta}(x)|x\rangle
\]

induces the Born distribution

\[
p_{\boldsymbol\theta}(x)
=|\psi_{\boldsymbol\theta}(x)|^2.
\]

Training attempts to make this distribution approximate a target data distribution.

## 3. Training objectives

Possible objectives include

- maximum likelihood,
- KL divergence when estimable,
- moment matching,
- maximum mean discrepancy,
- adversarial losses,
- and optimal-transport-inspired objectives.

The difficulty is that probabilities or likelihood gradients may be expensive to evaluate even if sampling is easy.

## 4. Quantum GANs

A quantum generative adversarial framework can assign quantum or classical roles to generator and discriminator. For example, a quantum generator may prepare states or samples while a discriminator attempts to distinguish generated from real data.

The phrase “QGAN” therefore covers multiple architectures; one must specify which components are quantum and what data type is generated.

## 5. Quantum data generation

A particularly natural setting is generative modeling of quantum states. The target may be a family of many-body states, a noisy device distribution, or outputs of a quantum process. Here a quantum generator can represent the target natively without a full classical state description.

## 6. Advantage questions

Potential advantages could arise in

- compact representation,
- sampling complexity,
- preparation of quantum states that are classically hard to sample,
- or learning directly in quantum state space.

However, hard-to-sample output does not automatically imply useful learning. One must establish that the trained distribution solves a meaningful generative task and that training itself is efficient.

## References

1. S. Lloyd and C. Weedbrook, "Quantum generative adversarial learning," *Phys. Rev. Lett.* 121, 040502 (2018). https://doi.org/10.1103/PhysRevLett.121.040502
2. M. Benedetti et al., "A generative modeling approach for benchmarking and training shallow quantum circuits," *npj Quantum Inf.* 5, 45 (2019). https://doi.org/10.1038/s41534-019-0157-8
