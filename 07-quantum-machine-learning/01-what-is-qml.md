# What Is Quantum Machine Learning?

## 1. Scope

Quantum machine learning (QML) studies learning problems in which **quantum information processing, quantum models, quantum data, or quantum access models** play a substantive role.

It is a research field, not a single algorithm.

QML includes both

```text
using quantum systems to perform learning
```

and

```text
learning properties of quantum systems.
```

These two directions overlap but are not identical.

## 2. Learning objectives

After this chapter, you should be able to:

- define QML without reducing it to variational circuits,
- classify QML problems by data type and computational model,
- distinguish training data access from model architecture,
- write a generic supervised quantum model mathematically,
- identify encoding, hypothesis class, measurement, loss, and optimizer as separate components,
- distinguish training complexity from inference complexity,
- identify multiple notions of quantum learning advantage,
- and formulate a QML problem using explicit resource assumptions.

## 3. A machine-learning problem first

Before introducing anything quantum, a learning problem requires:

- an input space $\mathcal X$,
- an output/target space $\mathcal Y$,
- a data-generating distribution or experiment,
- a hypothesis/model class $\mathcal F$,
- a loss function,
- a training procedure,
- a success criterion.

For supervised learning, a classical predictor is

```math
f_\theta:
\mathcal X\rightarrow\mathcal Y.
```

Training often minimizes empirical risk

```math
\widehat R_S(\theta)
=
\frac1m
\sum_{i=1}^{m}
\ell(f_\theta(x_i),y_i).
```

A quantum learner changes one or more components of this pipeline.

## 4. Four broad QML settings

A useful first taxonomy separates the nature of the data and the processing.

### Classical data, quantum processing

Input begins as classical information:

```math
x\in\mathcal X.
```

It must be encoded into a quantum system before quantum processing.

Typical examples:

- variational quantum classifiers,
- quantum kernels,
- quantum generative models for classical distributions.

### Quantum data, quantum processing

The learner directly receives quantum objects such as

```math
\rho_x,
```

```math
|\psi_x\rangle,
```

or access to a channel

```math
\mathcal E_x.
```

Here the learner may preserve coherence that would be lost by immediate measurement.

### Quantum-generated data, classical learning

A quantum experiment produces classical measurement records

```math
y_1,y_2,\ldots,y_N,
```

which are then processed by an ordinary classical learner.

Many scientifically important quantum-learning tasks use this pipeline without requiring a quantum learning model.

### Hybrid quantum-classical learning

A pipeline can combine:

```text
classical preprocessing
-> quantum encoding
-> quantum dynamics
-> measurement
-> classical postprocessing
-> classical optimizer.
```

Most practical QML architectures are hybrid in some sense.

## 5. Standard variational QML pipeline

A common supervised model starts with

```math
|0\rangle^{\otimes n}.
```

A data-encoding unitary prepares

```math
|\phi(x)\rangle
=
U_\phi(x)|0\rangle^{\otimes n}.
```

A trainable circuit then gives

```math
|\psi(x,\theta)\rangle
=
U(\theta)|\phi(x)\rangle.
```

Finally, an observable $M$ produces

```math
f_\theta(x)
=
\langle\psi(x,\theta)|M|\psi(x,\theta)\rangle.
```

Equivalently,

```math
f_\theta(x)
=
\langle0|
U_\phi^\dagger(x)
U^\dagger(\theta)
M
U(\theta)
U_\phi(x)
|0\rangle.
```

This is one important family of QML models, but it is not the definition of QML.

## 6. More general channel model

The unitary assumption can be relaxed.

A general parameterized quantum learner can be written

```math
\rho_x
\xrightarrow{\mathcal E_\theta}
\sigma_{x,\theta}
\xrightarrow{\{E_y\}}
y.
```

Prediction probabilities are

```math
p_\theta(y|x)
=
\mathrm{Tr}
\left[
E_y
\mathcal E_\theta(\rho_x)
\right].
```

The map $\mathcal E_\theta$ may include:

- unitary gates,
- noise or dissipation,
- resets,
- mid-circuit measurements,
- adaptive control,
- interactions with ancillas.

This channel-level description is more general than a PQC-only definition.

## 7. The measurement is part of the model

In many QML descriptions, the trainable circuit receives most attention while the readout is treated as fixed.

But the prediction depends jointly on state and measurement:

```math
p(y)
=
\mathrm{Tr}(E_y\rho).
```

One can therefore imagine learning:

- the state preparation,
- the channel,
- the measurement,
- or several of these simultaneously.

This is important when searching for QML architectures beyond standard VQCs.

## 8. Hypothesis class

A QML architecture induces a family of functions or conditional distributions.

For expectation-value models,

```math
\mathcal F
=
\left\{
f_\theta(x):\theta\in\Theta
\right\}.
```

For probabilistic models,

```math
\mathcal P
=
\left\{
p_\theta(y|x):\theta\in\Theta
\right\}.
```

The central learning-theory questions are therefore familiar:

- What can the class represent?
- Can it be optimized?
- How many examples are required?
- Does it generalize?
- Can a classical model represent the same class efficiently?

## 9. Training loss

A classifier may use cross-entropy,

```math
\mathcal L(\theta)
=
-\frac1m
\sum_i
\log p_\theta(y_i|x_i).
```

A regressor may use squared loss,

```math
\mathcal L(\theta)
=
\frac1m
\sum_i
\left(
f_\theta(x_i)-y_i
\right)^2.
```

A quantum-state learner may instead optimize fidelity or an information-theoretic objective.

Thus the same quantum model family can support very different learning semantics depending on the loss.

## 10. Training versus inference

Training cost and inference cost should be separated.

A model may require expensive training but cheap prediction, or the reverse.

For a variational model, training can involve

```math
N_{\mathrm{epochs}}
\times
N_{\mathrm{data}}
\times
N_{\mathrm{gradient\ settings}}
\times
N_{\mathrm{shots}}.
```

After training, one prediction may require only a few circuit evaluations.

A quantum advantage claim should specify which stage is being improved.

## 11. Quantum kernels

Quantum kernel methods often do not train a parameterized quantum circuit.

A quantum processor estimates

```math
K(x,x')
```

and the learning optimization can remain classical.

Therefore

```math
\text{QML}
\not\subset
\text{variational PQCs only}.
```

## 12. Quantum generative learning

A quantum model can learn a distribution rather than a label function.

Measurement of

```math
|\psi_\theta\rangle
=
\sum_x\psi_\theta(x)|x\rangle
```

produces

```math
p_\theta(x)
=
|\psi_\theta(x)|^2.
```

This creates quantum Born machines and other generative architectures.

## 13. Quantum reservoir computing

A quantum system can act as a fixed nonlinear dynamical feature generator while only a classical readout is trained.

This is structurally different from a fully trainable PQC.

It also raises a different advantage question: whether physical quantum dynamics provide useful temporal features at favorable cost.

## 14. Quantum reinforcement learning

In quantum RL, the quantum component can appear in:

- policy representation,
- value estimation,
- environment access,
- coherent interaction protocols,
- or the environment itself.

A “quantum RL” label is incomplete until these roles are specified.

## 15. Learning from quantum data

A particularly natural QML setting is

```math
\rho
\rightarrow
\text{quantum learner}
\rightarrow
\text{prediction}.
```

Possible tasks include:

- state discrimination,
- observable prediction,
- phase recognition,
- Hamiltonian learning,
- process learning,
- channel discrimination.

Here quantum processing may avoid the information loss caused by first converting all quantum data to classical measurement transcripts.

## 16. The access model is part of the problem

Two algorithms can appear to solve the same learning task while receiving fundamentally different inputs.

Examples of access include:

```text
classical samples
random classical queries
coherent oracle queries
QRAM-style access
copies of a quantum state
adaptive experiments
coherent quantum memory across examples.
```

A complexity comparison is meaningful only when these access models are matched or their differences are explicitly priced.

## 17. What can “quantum advantage” mean?

Different papers use the word advantage for different resources.

Possible meanings include:

### Runtime advantage

```math
T_Q(n)
<
T_C(n)
```

asymptotically or in a defined practical regime.

### Query advantage

Fewer calls to a black-box oracle.

### Sample or copy advantage

Fewer training examples, quantum-state copies, or physical experiments.

### Communication advantage

Less information exchanged between distributed parties.

### Representational advantage

A quantum model represents a target compactly while a restricted classical model requires much larger size.

### Approximation advantage

For the same resource budget, the quantum model achieves lower error.

These are distinct claims.

## 18. Representation is not learning advantage

Suppose a quantum circuit can represent a function using polynomial size while a particular classical architecture requires exponential size.

That establishes a representational separation only if proved under the specified model classes.

To obtain an end-to-end learning advantage, one still needs efficient:

- data access,
- training,
- measurement,
- inference.

Thus

```math
\text{representation advantage}
\not\Rightarrow
\text{training advantage}.
```

## 19. Benchmark hierarchy

A useful hierarchy of evidence is:

```text
quantum model runs
<
quantum model fits data
<
quantum model beats one baseline
<
advantage persists under tuned strong baselines
<
advantage persists under matched resource accounting
<
scaling separation
<
proved separation under explicit assumptions.
```

The levels should not be presented as interchangeable.

## 20. Classical baselines

The strongest classical competitor depends on task structure.

Relevant baselines can include:

- linear/logistic models,
- classical kernels,
- random features,
- neural networks,
- tensor networks,
- graph neural networks,
- classical shadows,
- specialized physics algorithms,
- quantum-inspired algorithms.

A small generic neural network is not a universal classical baseline.

## 21. Common misconceptions

### “QML means putting a neural network on a quantum computer.”

No. QML includes kernels, learning theory, reservoir methods, quantum-data learning, process learning, and more.

### “Any trainable PQC is automatically a QNN.”

Terminology varies. The architecture should be defined explicitly.

### “Exponential Hilbert-space dimension gives exponential learning capacity for free.”

No. Encoding, measurement, trainability, and accessible information constrain usefulness.

### “Higher quantum-model accuracy proves quantum advantage.”

Not without strong baselines and fair resource accounting.

### “Classical data and quantum data are equivalent inputs once encoded.”

No. Encoding classical data can be costly, while native quantum data may contain information that is lost through classicalization.

## 22. A rigorous QML specification template

For every QML problem, write:

```text
Task:
Data type:
Data-access model:
Quantum representation:
Hypothesis class:
Trainable objects:
Measurement/readout:
Loss:
Optimizer:
Training resource:
Inference resource:
Classical baseline:
Claimed quantum resource:
Success criterion:
```

If several fields are missing, the advantage claim is probably under-specified.

## 23. Worked example: binary variational classifier

Let

```math
x\in\mathbb R^d,
\qquad
y\in\{-1,+1\}.
```

Encode

```math
|\phi(x)\rangle
=
U_\phi(x)|0\rangle^{\otimes n}.
```

Apply trainable circuit $W(\theta)$ and measure $Z_1$:

```math
f_\theta(x)
=
\langle Z_1\rangle_{x,\theta}.
```

Predict

```math
\hat y
=
\mathrm{sign}(f_\theta(x)).
```

A complete complexity analysis must still ask:

- How expensive is $U_\phi(x)$?
- How many shots estimate $f_\theta(x)$?
- How many quantum evaluations are required for training?
- What classical models use the same data and preprocessing?

The circuit formula alone does not answer whether the model is useful.

## 24. Research strategy

A stronger QML research strategy is often

```text
learning task
-> identify information bottleneck
-> identify possible quantum resource
-> define strongest restricted/classical competitor
-> search for a separation
-> design architecture around the separation.
```

This reverses the weaker workflow

```text
choose PQC
-> choose benchmark dataset
-> hope for higher accuracy.
```

## 25. Exercises

### Conceptual

1. Give three QML problems that do not require a trainable PQC.
2. Why must the data-access model be included in a complexity claim?
3. Distinguish representational advantage from sample-complexity advantage.
4. Why can learning from native quantum data be conceptually different from encoding classical vectors?

### Computational

5. Write the Born probabilities for a binary classifier using a two-outcome POVM $\{E_0,E_1\}$.
6. Suppose training uses 1000 data points, 50 parameters, two parameter-shift settings per parameter, and 100 shots per setting. Estimate the raw circuit-shot count for one full-batch gradient step, ignoring observable grouping.
7. For a model output $f_\theta(x)=\langle Z\rangle$, show that $f_\theta(x)\in[-1,1]$.
8. Convert that expectation into a Bernoulli probability through $p=(1+f)/2$.

### Research-oriented

9. Choose a QML paper and fill in the rigorous specification template above.
10. Design a task where the trainable object is the measurement rather than the circuit.
11. Formulate a learning problem in which a quantum channel, rather than a state or scalar function, is the prediction target.
12. What would it mean to identify the *minimal genuinely quantum primitive* required for a learning advantage?

## 26. Key takeaways

- QML is a field spanning quantum models, quantum data, learning theory, and hybrid algorithms.
- Variational QML is one family, not the definition of QML.
- Data access, encoding, hypothesis class, measurement, loss, and optimizer are separate components.
- Quantum advantage can refer to runtime, queries, samples, communication, representation, or approximation quality.
- A useful QML claim requires explicit access assumptions and strong classical baselines.
- Native quantum-data tasks can provide fundamentally different opportunities from classical-data encoding.
- Research should begin from the learning bottleneck and candidate quantum resource, not from a circuit architecture alone.

## References

1. J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
2. M. Schuld and F. Petruccione, *Supervised Learning with Quantum Computers*, Springer, 2018. https://doi.org/10.1007/978-3-319-96424-9
3. M. Cerezo et al., "Challenges and opportunities in quantum machine learning," *Nature Computational Science* 2, 567–576 (2022). https://doi.org/10.1038/s43588-022-00311-3
