# What Is Quantum Machine Learning?

## 1. Scope

Quantum machine learning (QML) is the intersection of quantum information processing and statistical learning. It includes both

- using quantum systems to solve learning problems, and
- learning properties of quantum systems from classical or quantum observations.

There is no single canonical “QML algorithm.”

## 2. Four broad settings

A useful taxonomy is based on whether data and processing are classical or quantum.

### Classical data, quantum processing

A classical input

```math
x\in\mathcal X
```

is encoded into a quantum state or circuit, processed quantum mechanically, and measured.

### Quantum data, quantum processing

The learner directly receives states or channels such as

```math
\rho_x,
\qquad
\mathcal E_x.
```

This avoids first converting all quantum information into a classical description.

### Quantum-generated data, classical learning

A classical learner can analyze measurement outcomes from a quantum experiment. Many quantum-science tasks use this pipeline without requiring a quantum learning model.

### Hybrid learning

Quantum and classical components can be interleaved: classical feature extraction, quantum embedding, quantum measurement, and classical postprocessing can all coexist.

## 3. Standard variational pipeline

A common supervised QML model is

```math
x
\xrightarrow{U_\phi(x)}
|\phi(x)\rangle
\xrightarrow{U(\boldsymbol\theta)}
|\psi(x,\boldsymbol\theta)\rangle
\xrightarrow{M}
f_{\boldsymbol\theta}(x).
```

The prediction is often an expectation value

```math
f_{\boldsymbol\theta}(x)
=
\langle0|
U_\phi^\dagger(x)U^\dagger(\boldsymbol\theta)
M
U(\boldsymbol\theta)U_\phi(x)
|0\rangle.
```

A classical optimizer updates $\boldsymbol\theta$ using a training loss.

This is **variational QML**, not the definition of QML itself.

## 4. Other QML paradigms

Important families include

- quantum kernel methods,
- quantum generative models,
- quantum reservoir computing,
- quantum reinforcement learning,
- quantum learning theory,
- quantum-state and process learning,
- and hybrid architectures using measurements, channels, or analog dynamics.

## 5. What counts as a quantum advantage?

Possible notions include improvement in

- runtime,
- query complexity,
- sample complexity,
- communication complexity,
- memory,
- representational efficiency,
- or achievable statistical error under a specified data-access model.

Higher accuracy than a weak classical baseline is not sufficient evidence.

## 6. Central research questions

QML research is fundamentally about questions such as

```math
\boxed{
\text{Which learning tasks contain a useful quantum resource?}
}
```

and

```math
\boxed{
\text{Under what access model is that resource unavailable or expensive classically?}
}
```

These questions are often more informative than asking whether a particular circuit architecture beats a neural network on a small benchmark.

## References

1. J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
2. M. Schuld and F. Petruccione, *Supervised Learning with Quantum Computers*, Springer, 2018. https://doi.org/10.1007/978-3-319-96424-9
