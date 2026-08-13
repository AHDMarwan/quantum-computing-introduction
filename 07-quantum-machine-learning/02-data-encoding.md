# Data Access and Quantum Encoding

## 1. Encoding is part of the learning algorithm

When the raw data are classical, a quantum learner must specify how those data enter the quantum system.

A feature map is a transformation

```math
x
\longmapsto
\rho(x),
```

or, for a pure-state encoding,

```math
x
\longmapsto
|\phi(x)\rangle.
```

This transformation is not merely a visualization step. It determines:

- which information is retained,
- which geometry the learner sees,
- which functions become easy or difficult to represent,
- how many qubits and gates are required,
- and whether a claimed quantum speedup survives end-to-end resource accounting.

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish data representation from data access,
- compare basis, angle, amplitude, Hamiltonian, and repeated encodings,
- explain why compact qubit count does not imply cheap state preparation,
- formulate classical sample, oracle, coherent-oracle, QRAM-like, and quantum-state access models,
- derive simple quantum kernels from feature maps,
- explain how data re-uploading changes the function class,
- identify encoding-induced concentration and information loss,
- and audit QML complexity claims for hidden input-loading assumptions.

## 3. Data representation versus data access

Two distinct questions must be separated.

### Representation

How is one input represented after it is available to the quantum processor?

For example,

```math
x
\mapsto
|\phi(x)\rangle.
```

### Access

How does the processor obtain the components of $x$ in the first place?

Examples include:

```text
explicit vector stored classically
sample access
data stream
random-access memory
classical query oracle
coherent query oracle
copies of a quantum state.
```

A state representation may be compact while the access procedure required to prepare it is expensive.

## 4. Basis encoding

For a binary string

```math
x=(x_1,\ldots,x_n)
\in
\{0,1\}^n,
```

basis encoding is

```math
x
\longmapsto
|x_1x_2\cdots x_n\rangle.
```

Starting from $|0\rangle^{\otimes n}$, one applies an $X$ gate to qubit $j$ whenever

```math
x_j=1.
```

The preparation cost is therefore linear in the number of encoded bits in the straightforward implementation.

### Strengths

- simple,
- exact for discrete binary data,
- easy computational-basis readout.

### Limitations

- one qubit per bit,
- no compression of generic binary inputs,
- basis states are mutually orthogonal, so similarity is not automatically encoded geometrically.

## 5. Angle encoding

A real feature $x_j$ can control a rotation:

```math
|\phi(x)\rangle
=
\bigotimes_{j=1}^{d}
R_y(x_j)|0\rangle.
```

For one feature,

```math
R_y(x)|0\rangle
=
\cos\frac{x}{2}|0\rangle
+
\sin\frac{x}{2}|1\rangle.
```

Thus a classical scalar becomes a quantum amplitude through a physically simple gate parameter.

A common generalized encoding is

```math
R_y(sx_j+b),
```

where the scaling $s$ and offset $b$ determine which region of the periodic quantum feature map is used.

## 6. Periodicity and preprocessing

Rotation encoding is periodic. For example,

```math
R_y(x+2\pi)
```

represents the same Bloch-sphere rotation as $R_y(x)$ up to the expected unitary periodicity/global-phase convention.

Therefore two numerically distant classical inputs may become identical or nearly identical quantum states if feature scaling is poorly chosen.

This means normalization is part of model design:

```text
classical feature scale
-> quantum rotation scale
-> feature-state geometry.
```

Standardizing data is not a neutral preprocessing detail when the standardized values directly become physical angles.

## 7. Worked example: angle-encoding geometry

For one-dimensional data, define

```math
|\phi(x)\rangle
=
R_y(x)|0\rangle.
```

The overlap is

```math
\langle\phi(x)|\phi(x')\rangle
=
\cos\left(\frac{x-x'}{2}\right).
```

Therefore the fidelity kernel is

```math
K(x,x')
=
\cos^2\left(\frac{x-x'}{2}\right).
```

The encoding has already imposed a notion of similarity before any trainable circuit is added.

This is a central QML principle:

> The data embedding itself is an inductive bias.

## 8. Amplitude encoding

Let

```math
x
=
(x_0,\ldots,x_{d-1})
\in
\mathbb C^d.
```

After normalization,

```math
|x\rangle
=
\frac{1}{\|x\|_2}
\sum_{j=0}^{d-1}
x_j|j\rangle.
```

Only

```math
n
=
\lceil\log_2d\rceil
```

qubits are needed to represent the basis index.

This exponential compression in **qubit count** is often visually attractive.

But it does not imply exponential compression in **preparation cost**.

## 9. State-preparation caveat

A generic normalized vector has order $d$ independent real degrees of freedom.

Preparing an arbitrary state

```math
\sum_{j=0}^{d-1}x_j|j\rangle
```

from a fixed reference state can therefore require resources scaling with $d$ in generic circuit models.

Thus

```math
O(\log d)
\text{ qubits}
```

can coexist with

```math
O(d)
\text{ input/preparation work}.
```

Any algorithm claiming polylogarithmic complexity after amplitude encoding must specify how the state is supplied or prepared efficiently.

## 10. Structured amplitude preparation

Amplitude encoding can still be useful when the vector has structure.

Examples include cases where:

- the amplitudes are generated by an efficient classical formula,
- a compact circuit family prepares the state,
- the data are outputs of another quantum process,
- a specialized memory architecture provides coherent access,
- the state has sparse or tensor-product structure.

The correct question is not

> Is amplitude encoding efficient?

but rather

> Under which data-generation or access model is this particular amplitude state efficient to prepare?

## 11. Coherent oracle access

A classical value oracle can be represented reversibly as

```math
O_x|j,z\rangle
=
|j,z\oplus x_j\rangle
```

for discrete data.

A coherent quantum algorithm can query a superposition of indices:

```math
\sum_j\alpha_j|j\rangle|0\rangle
\longmapsto
\sum_j\alpha_j|j\rangle|x_j\rangle.
```

This is a stronger interface than reading one classical entry at a time.

If the classical baseline is not granted a comparable access model, an apparent speedup may actually be an access-model separation.

## 12. QRAM-style assumptions

Quantum random-access memory is often invoked informally to justify transformations such as

```math
\sum_j\alpha_j|j\rangle|0\rangle
\longmapsto
\sum_j\alpha_j|j\rangle|x_j\rangle.
```

For complexity analysis, several questions matter:

- Who built the memory?
- What is the cost of loading the dataset?
- Is the memory static and reused across many queries?
- What hardware resources scale with dataset size?
- What noise model affects coherent access?

Treating QRAM as a single unit-cost gate can hide substantial physical and preprocessing cost.

## 13. Sample access versus query access

In ordinary supervised learning, a learner might receive samples

```math
(x_i,y_i)
\sim
\mathcal D.
```

A quantum query model might instead provide coherent access to an oracle or distribution state.

These are different learning models.

A valid comparison must specify whether the resource is:

```text
number of examples
number of oracle queries
number of state copies
runtime per query
memory construction cost.
```

## 14. Native quantum data

If the input is already a quantum state

```math
\rho_x,
```

there may be no classical data-loading step.

This can fundamentally change the advantage question.

The alternatives may be:

```text
keep rho_x quantum and process coherently
```

versus

```text
measure rho_x
-> store a classical transcript
-> learn classically.
```

The latter can irreversibly discard information depending on the measurement protocol.

## 15. Phase encoding

Classical data can also enter as phases. For example,

```math
U_\phi(x)
=
e^{i\phi(x)Z}.
```

On a superposition state, the phase can later affect measurement through interference.

This is especially natural when the model is built around Fourier structure.

Repeated phase encodings can generate increasingly rich frequency spectra in the classical input variables.

## 16. Hamiltonian encoding

Features can parameterize a Hamiltonian:

```math
H(x)
=
\sum_jx_jH_j.
```

Then the feature map may be

```math
U(x)
=
e^{-itH(x)}.
```

This representation is natural when data correspond to physical control parameters or when analog quantum dynamics are used as the embedding.

The encoding cost then depends on implementing the data-dependent Hamiltonian and evolution time.

## 17. Data re-uploading

Instead of inserting data only once, a model can alternate data-dependent and trainable blocks:

```math
U(x,\theta)
=
W_L(\theta_L)V_L(x)
\cdots
W_1(\theta_1)V_1(x).
```

This is data re-uploading.

Repeated appearance of $x$ changes the function class even when the number of qubits is fixed.

## 18. Fourier viewpoint of data encoding

For rotation-based encodings, expectation-value models often produce functions that can be expanded in Fourier-like components:

```math
f_\theta(x)
=
\sum_{\omega\in\Omega}
c_\omega(\theta)
e^{i\omega x}.
```

The encoding generators determine the accessible frequency set $\Omega$, while trainable gates determine coefficients and interference among those frequencies.

Repeated data encoding can enlarge the accessible spectrum.

This gives a precise reason why encoding architecture changes expressivity.

## 19. Encoding as feature geometry

The quantum feature map induces similarities such as

```math
K(x,x')
=
\mathrm{Tr}
\left[
\rho(x)\rho(x')
\right]
```

or pure-state fidelity

```math
K(x,x')
=
|\langle\phi(x)|\phi(x')\rangle|^2.
```

The learning value of the encoding depends on whether target labels are simple relative to this geometry.

A classically hard feature map that sends all training examples to nearly indistinguishable states can still be useless.

## 20. Encoding-induced concentration

Suppose random data points produce feature states satisfying

```math
K(x,x')
\approx
c
```

for almost all pairs $x\neq x'$.

Then the kernel matrix can become close to a nearly constant matrix.

Distinguishing meaningful pairwise structure may require estimating tiny deviations from $c$ with high precision.

Thus high-dimensional feature maps can suffer from **concentration**.

The exponential Hilbert space can become an obstacle rather than an advantage.

## 21. Information-preserving versus information-destroying encodings

An encoding can lose relevant information.

If

```math
\rho(x)=\rho(x')
```

for two inputs with different labels,

```math
y(x)\neq y(x'),
```

then no downstream quantum circuit or measurement can perfectly distinguish those examples.

The loss happened at the encoding stage.

More generally, data processing implies that later quantum channels cannot recover information that the encoding has completely erased.

## 22. Redundant encoding

At the opposite extreme, an encoding may retain far more information than the task requires.

This can increase:

- circuit size,
- measurement complexity,
- sensitivity to irrelevant features,
- concentration risk.

A useful feature map can therefore be viewed as a form of **task-relevant compression** rather than maximum information loading.

## 23. Quantum sufficient-statistic viewpoint

Suppose the target is $Y$ and the raw data are $X$.

Instead of asking how to encode all of $X$, one can seek a quantum representation $Q$ that retains only the information needed for prediction.

Conceptually:

```math
X
\longrightarrow
Q
\longrightarrow
Y.
```

A research objective might trade representation size against predictive information, for example using information quantities such as

```math
I(X:Q)
```

and

```math
I(Q:Y).
```

This reverses the common narrative that QML should always exploit the largest possible Hilbert space.

## 24. Encoding cost in end-to-end complexity

A useful total-cost decomposition is

```math
C_{\mathrm{QML}}
=
C_{\mathrm{access}}
+
C_{\mathrm{encode}}
+
C_{\mathrm{model}}
+
C_{\mathrm{measure}}
+
C_{\mathrm{train}}
+
C_{\mathrm{classical\ post}}.
```

If

```math
C_{\mathrm{encode}}
```

already scales linearly with a high-dimensional input, a later logarithmic-dimensional circuit does not erase that cost.

## 25. Dequantization and access assumptions

Some quantum algorithms appear exponentially faster only because they assume a strong input model such as coherent amplitude access.

A quantum-inspired classical algorithm may recover much of the speedup if granted analogous sampling/query access.

This motivates the audit question:

> Is the advantage caused by quantum processing, or by a stronger data interface?

The answer must be established rather than assumed.

## 26. Common misconceptions

### “Amplitude encoding gives exponential data compression.”

It gives exponential compression in qubit **representation size**, but generic state preparation can still scale linearly in the vector dimension.

### “Encoding is preprocessing, so it does not count.”

It counts whenever the quantum computation requires it.

### “More complicated embeddings are better.”

Not if they destroy target-relevant geometry or cause concentration.

### “QRAM means free random access to a classical dataset.”

No. Construction, loading, hardware size, reuse assumptions, and noise all matter.

### “If the data are quantum, there is no data-access cost.”

There is still a cost in producing, transmitting, storing, or obtaining copies of the quantum data; it is simply a different resource model.

## 27. A data-access audit template

For every QML proposal, record:

```text
Raw data type:
Dataset size:
Feature dimension:
Access primitive:
State-preparation circuit:
Preparation gate complexity:
Ancilla/qubit cost:
Can preparation be reused?
Number of data calls per prediction:
Number of data calls during training:
Equivalent classical access model:
Information discarded by encoding:
```

This table should be completed before quoting a quantum speedup.

## 28. Worked comparison: angle versus amplitude encoding

Suppose

```math
x\in\mathbb R^{1024}.
```

### Angle encoding

A direct one-feature-per-qubit map may require order

```math
1024
```

qubits and roughly one parameterized rotation per feature.

### Amplitude encoding

Only

```math
\log_2(1024)=10
```

qubits are needed for the state vector index.

But a generic arbitrary amplitude state may require order

```math
1024
```

preparation work.

The tradeoff is therefore not “1024 versus 10 operations”; it is closer to

```text
many qubits + simple loading
versus
few qubits + potentially difficult coherent state preparation.
```

The better encoding depends on hardware, structure, reuse, and the downstream algorithm.

## 29. Connections

Data encoding connects directly to:

- quantum kernels,
- variational QML expressivity,
- Fourier analysis of QML models,
- trainability and concentration,
- data-loading dequantization,
- quantum learning theory,
- learning from native quantum data.

It is one of the first places to look when a proposed QML advantage seems unexpectedly large.

## 30. Exercises

### Conceptual

1. Distinguish data representation from data access.
2. Why does amplitude encoding reduce qubit count without guaranteeing reduced total input cost?
3. How can feature scaling change the geometry of angle encoding?
4. Why can an encoding be too expressive or too information preserving for a particular task?

### Computational

5. Derive the one-dimensional angle-encoding kernel

```math
K(x,x')
=
\cos^2\left(\frac{x-x'}{2}\right).
```
6. How many qubits are required to amplitude-encode vectors of dimensions $256$, $1024$, and $10^6$ after zero padding to powers of two?
7. For a general one-qubit density matrix, apply complete dephasing and identify which information is lost.
8. If one data point requires $d$ rotation gates and a training routine evaluates the circuit $R$ times, estimate the total number of data-dependent gate applications.

### Research-oriented

9. A paper claims exponential speedup after assuming QRAM loading. Write the minimum set of questions needed to evaluate whether the access assumption is fair.
10. Propose a quantum encoding optimized for a symmetry of a physical dataset rather than generic expressivity.
11. Design an experiment comparing a highly scrambling feature map with a local feature map using kernel concentration and downstream generalization.
12. Formulate a notion of quantum sufficient statistic for a supervised quantum-data problem.

## 31. Key takeaways

- Data access and data representation are distinct resources.
- Basis, angle, amplitude, phase, Hamiltonian, and repeated encodings impose different geometry and cost.
- Compact qubit representation does not imply cheap state preparation.
- Encoding determines the function class before trainable layers are considered.
- High-dimensional quantum embeddings can suffer from concentration and information-access problems.
- Native quantum data create a different access model from classically encoded data.
- End-to-end QML complexity must count data access and preparation explicitly.
- A useful encoding should preserve target-relevant information, not necessarily all available information.

## References

1. V. Havlíček et al., "Supervised learning with quantum-enhanced feature spaces," *Nature* 567, 209–212 (2019). https://doi.org/10.1038/s41586-019-0980-2
2. M. Schuld, R. Sweke, and J. J. Meyer, "Effect of data encoding on the expressive power of variational quantum-machine-learning models," *Physical Review A* 103, 032430 (2021). https://doi.org/10.1103/PhysRevA.103.032430
3. E. Tang, "A quantum-inspired classical algorithm for recommendation systems," *Proceedings of STOC* (2019). https://doi.org/10.1145/3313276.3316310
4. H.-Y. Huang et al., "Power of data in quantum machine learning," *Nature Communications* 12, 2631 (2021). https://doi.org/10.1038/s41467-021-22539-9
