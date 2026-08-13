# Generalization in Quantum Machine Learning

## 1. Training accuracy is not learning

A model generalizes when performance on unseen data is controlled by information obtained from the training set rather than by memorization alone.

For a loss $\ell$, define population risk

```math
R(\theta)
=
\mathbb E_{(x,y)\sim\mathcal D}
\ell(f_\theta(x),y)
```

and empirical risk

```math
\widehat R_S(\theta)
=
\frac1m\sum_{i=1}^m
\ell(f_\theta(x_i),y_i).
```

The generalization gap is

```math
R(\theta)-\widehat R_S(\theta).
```

## 2. QML does not escape statistical learning theory

A quantum model can overfit. The fact that its Hilbert space is exponentially large does not imply either good or bad generalization by itself. Relevant quantities include

- effective hypothesis complexity,
- norm or parameter constraints,
- data geometry,
- measurement structure,
- number of trainable gates,
- information contained in the training procedure,
- and noise/regularization.

## 3. Capacity and trainable parameters

Generalization bounds for parameterized quantum models can depend polynomially on the number of trainable gates or parameters under suitable assumptions. This shows that Hilbert-space dimension alone is not the right capacity measure.

## 4. Quantum kernels

For kernel methods, generalization is governed by the kernel matrix, margins, target alignment, effective dimension, and sample distribution. A classically hard kernel can still generalize poorly if it maps examples into an uninformative geometry.

## 5. Beyond i.i.d. sample generalization

Quantum learning suggests broader notions of extrapolation, such as

- new system sizes,
- new Hamiltonian parameters,
- unseen measurement settings,
- unseen noise channels,
- new graph sizes,
- or new times in a dynamical process.

These forms can be scientifically more relevant than random train/test splits.

## 6. Symmetry and locality as inductive bias

If the target law is invariant under a group $G$, an equivariant or invariant model can reduce unnecessary hypothesis complexity. Similarly, local architectures can transfer across system size when the learned rule is local.

This suggests a research principle:

```math
\text{use physical structure as inductive bias rather than maximizing generic expressivity}.
```

## References

1. M. C. Caro et al., "Generalization in quantum machine learning from few training data," *Nat. Commun.* 13, 4919 (2022). https://doi.org/10.1038/s41467-022-32550-3
2. L. Banchi, J. Pereira, and S. Pirandola, "Generalization in quantum machine learning: A quantum information standpoint," *PRX Quantum* 2, 040321 (2021). https://doi.org/10.1103/PRXQuantum.2.040321
