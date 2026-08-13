# Trainability in Quantum Machine Learning

## 1. What trainability means

Trainability is the ability to extract enough optimization signal to efficiently locate a useful model within the chosen hypothesis class. It is distinct from expressivity and generalization.

A model can be

- expressive but untrainable,
- trainable but too weak,
- trainable and expressive but poorly generalizing,
- or well aligned on all three axes.

## 2. Gradient concentration

For a loss

$$
L(\boldsymbol\theta),
$$

a barren plateau can arise when

$$
\operatorname{Var}
\left[\partial_{\theta_j}L\right]
$$

decays exponentially with system size for the relevant parameter distribution and model family.

Resolving the sign of a gradient then requires exponentially increasing measurement precision.

## 3. Data-induced issues

In QML, trainability depends not only on circuit randomness but also on data encoding. Highly scrambling embeddings can map different examples into states whose measured statistics concentrate, reducing useful variation across the dataset.

Kernel concentration is the analogous phenomenon in quantum kernel methods.

## 4. Noise

Noise can suppress gradients and distinguishability as circuit depth grows. Increasing shots reduces sampling variance but does not eliminate systematic noise bias.

Thus

$$
\text{more shots}\not\Rightarrow\text{noise-free optimization}.
$$

## 5. Architectural strategies

Useful strategies include

- local costs,
- shallow circuits,
- structured initialization,
- layerwise training,
- symmetry-preserving circuits,
- parameter sharing,
- problem-inspired architectures,
- and avoiding unnecessary global randomization.

## 6. Initialization and data scale

The scale of encoded features and initial parameters can strongly affect optimization. Data normalization is not a trivial classical preprocessing detail when features directly determine quantum rotation angles or Hamiltonian evolution times.

## 7. Trainability as information flow

A useful interpretation is to ask whether a parameter perturbation creates a statistically detectable change in the measured output. If

$$
\rho_{\theta}
\approx
\rho_{\theta+\delta}
$$

under all measurements used by the loss, the optimizer has little information about the update direction.

This connects trainability to quantum Fisher information, distinguishability, locality, and measurement design.

## References

1. J. R. McClean et al., "Barren plateaus in quantum neural network training landscapes," *Nat. Commun.* 9, 4812 (2018). https://doi.org/10.1038/s41467-018-07090-4
2. M. Cerezo et al., "Cost function dependent barren plateaus in shallow parametrized quantum circuits," *Nat. Commun.* 12, 1791 (2021). https://doi.org/10.1038/s41467-021-21728-w
3. S. Wang et al., "Noise-induced barren plateaus in variational quantum algorithms," *Nat. Commun.* 12, 6961 (2021). https://doi.org/10.1038/s41467-021-27045-6
