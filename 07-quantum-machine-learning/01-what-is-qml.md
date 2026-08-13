# What Is Quantum Machine Learning?

## 1. Scope

Quantum machine learning (QML) is the broad area where **machine learning** and **quantum information processing** meet.

It can mean several different things:

- using a quantum computer as part of a learning algorithm,
- using trainable quantum models,
- using quantum systems to define kernels or feature maps,
- learning directly from quantum states or processes,
- or studying how learning theory changes when information is quantum.

QML is therefore **not one algorithm** and it is not equivalent to “training a quantum neural network.”

## 2. Learning objectives

After this chapter, you should be able to:

- explain what QML includes,
- distinguish classical-data and quantum-data learning,
- identify the main components of a QML pipeline,
- distinguish a PQC, VQC, QNN, and quantum kernel at a high level,
- explain the role of measurement in a quantum model,
- distinguish training from inference,
- and explain what “quantum advantage” can mean without overinterpreting it.

## 3. Start from machine learning

A supervised learning problem usually contains:

- an input space $\mathcal X$,
- a target space $\mathcal Y$,
- training examples $(x_i,y_i)$,
- a model $f_\theta$,
- a loss function,
- and a training procedure.

A classical model can be written as

```math
f_\theta:\mathcal X\rightarrow\mathcal Y.
```

Training adjusts $\theta$ so that predictions improve on the task.

QML changes one or more parts of this pipeline by introducing quantum states, quantum operations, quantum measurements, or quantum data.

## 4. Classical data with quantum processing

Suppose the input is a classical vector

```math
x\in\mathbb R^d.
```

Before a quantum processor can use it, the information must be encoded into a quantum state or quantum operation. A common form is

```math
|\phi(x)\rangle
=
U_\phi(x)|0\rangle^{\otimes n}.
```

A trainable circuit may then process the encoded state:

```math
|\psi(x,\theta)\rangle
=
U(\theta)|\phi(x)\rangle.
```

Finally, an observable $M$ is measured:

```math
f_\theta(x)
=
\langle\psi(x,\theta)|M|\psi(x,\theta)\rangle.
```

This is the standard variational-QML picture.

A useful diagram is

```text
classical input
→ quantum encoding
→ trainable quantum circuit
→ measurement
→ classical prediction
→ loss
→ optimizer
```

Not every QML method follows this structure, but it is an important starting point.

## 5. Quantum data

QML can also begin with data that are already quantum.

Examples include

```math
\rho,
\qquad
|\psi\rangle,
\qquad
\mathcal E,
\qquad
H.
```

The task may be to:

- distinguish quantum states,
- predict observables,
- classify phases of matter,
- learn a Hamiltonian,
- identify a quantum channel,
- or learn a dynamical process.

This setting is conceptually different from encoding a classical vector into qubits. The information is quantum from the beginning.

## 6. Four broad settings

A simple classification is:

### 6.1 Classical data, quantum processing

```text
classical data
→ quantum encoding
→ quantum model
→ classical output
```

Examples: variational classifiers and quantum kernels.

### 6.2 Quantum data, quantum processing

```text
quantum states or processes
→ quantum processing
→ prediction
```

Examples: state discrimination and learning from quantum experiments.

### 6.3 Quantum experiment, classical learning

```text
quantum experiment
→ measurement outcomes
→ classical machine learning
```

The learner itself may be completely classical.

### 6.4 Hybrid learning

A practical system may combine classical preprocessing, quantum circuits, measurements, and classical optimization.

Most real QML workflows are hybrid in some form.

## 7. The measurement is part of the model

A general quantum prediction can be written as

```math
p_\theta(y|x)
=
\mathrm{Tr}
\left[
E_y\,\mathcal E_\theta(\rho_x)
\right].
```

This separates three objects:

```text
input state
→ quantum transformation
→ measurement
```

where:

- $\rho_x$ represents the input,
- $\mathcal E_\theta$ is the quantum processing step,
- $E_y$ is a measurement effect associated with output $y$.

This form is more general than a unitary circuit followed by a fixed Pauli measurement.

## 8. Main QML families

### Variational quantum models

A parameterized quantum circuit is trained using a loss function and a classical optimizer.

### Quantum kernels

A quantum computer estimates a similarity such as

```math
K(x,x')
=
|\langle\phi(x)|\phi(x')\rangle|^2.
```

The final learning algorithm may then be classical, such as an SVM.

### Structured quantum models

Architectures such as QCNNs incorporate locality, hierarchy, symmetry, or graph structure.

### Quantum generative models

A quantum state can define a probability distribution through the Born rule:

```math
p_\theta(x)
=
|\langle x|\psi_\theta\rangle|^2.
```

### Quantum reservoir computing

A fixed quantum dynamical system generates features, while a simpler classical readout is trained.

### Quantum reinforcement learning

Quantum components can appear in policies, value models, environment interactions, or the environment itself.

### Learning from quantum data

The inputs are states, channels, Hamiltonians, or dynamical processes rather than ordinary classical vectors.

## 9. PQC, VQC, and QNN

These terms are often confused.

A **PQC** is a parameterized quantum circuit:

```math
U(\theta).
```

A **VQC**, in this repository, means a variational quantum classifier when the task is classification.

A **QNN** is a broad architecture-dependent term. Different papers use it differently.

A **VQA** is a variational quantum algorithm: the full hybrid optimization framework.

Therefore

```text
PQC = circuit object
VQA = optimization framework
VQC = a classifier using a variational quantum model
QNN = broad architectural terminology
QML = the whole field
```

The dedicated terminology chapter develops these distinctions in more detail.

## 10. Training and inference are different

Training a model may require many repeated circuit executions.

For example, a variational model can require repeated evaluation over

```text
data points
× optimizer steps
× gradient settings
× measurement shots
```

while inference after training may require only a small number of circuit evaluations.

Therefore training cost and prediction cost should be discussed separately.

## 11. Expressivity, trainability, and generalization

These three ideas are related but not identical.

### Expressivity

Can the model represent the target function or distribution?

### Trainability

Can useful parameter values be found efficiently enough?

### Generalization

Does the trained model perform well on unseen examples?

A model can be highly expressive but difficult to train. It can also train easily but generalize poorly.

## 12. What can quantum advantage mean?

The phrase “quantum advantage” can refer to several different resources:

- runtime,
- query complexity,
- number of samples or quantum-state copies,
- memory,
- communication,
- representation size,
- or approximation quality.

These meanings should not be mixed together.

For example, a quantum model using fewer parameters than one restricted classical model does not automatically imply a faster training algorithm.

The dedicated [Quantum Advantage in Learning](13-quantum-advantage.md) chapter develops this topic carefully.

## 13. Worked example: a binary variational classifier

Suppose

```math
x\in\mathbb R^d,
\qquad
y\in\{-1,+1\}.
```

Encode the data as

```math
|\phi(x)\rangle
=
U_\phi(x)|0\rangle^{\otimes n}.
```

Apply a trainable circuit

```math
|\psi(x,\theta)\rangle
=
W(\theta)|\phi(x)\rangle.
```

Measure $Z$ on the first qubit:

```math
f_\theta(x)
=
\langle Z_1\rangle_{x,\theta}.
```

Because the eigenvalues of $Z$ are $\pm1$,

```math
-1\le f_\theta(x)\le1.
```

A simple prediction rule is

```math
\hat y
=
\mathrm{sign}(f_\theta(x)).
```

This model contains several distinct design choices:

- how $x$ is encoded,
- which circuit $W(\theta)$ is used,
- which observable is measured,
- which loss is optimized,
- and how the parameters are updated.

Changing any of these can change the learning behavior.

## 14. Common misconceptions

### “QML means running a classical neural network on qubits.”

No. QML includes many methods that do not resemble neural networks.

### “Any parameterized circuit is automatically a QNN.”

Not necessarily. QNN is an overloaded architectural term.

### “A large Hilbert space automatically gives better learning.”

No. Useful learning also depends on encoding, measurement, trainability, data geometry, and the task.

### “If a quantum model has higher accuracy once, quantum advantage is proven.”

No. Performance depends on the comparison, resource budget, data, and experimental setup.

### “Classical data and quantum data are the same after encoding.”

No. Encoding classical information into a quantum state and receiving an unknown quantum state as the input are different information-access settings.

## 15. Exercises

### A. Conceptual

1. Give two QML examples that do not require a trainable PQC.
2. Explain the difference between classical data encoded into a quantum state and native quantum data.
3. Why is measurement part of the model rather than merely an implementation detail?
4. Distinguish expressivity, trainability, and generalization.
5. Give two different meanings of quantum advantage.

### B. Computational

6. For a binary measurement $\{E_0,E_1\}$, write the two Born probabilities for input state $\rho$.
7. Show that an expectation value of a Pauli observable lies in $[-1,1]$.
8. Convert an expectation value $f\in[-1,1]$ into a Bernoulli probability using $p=(1+f)/2$.
9. Suppose one model evaluation uses 200 shots and a training loop evaluates the circuit 5000 times. How many circuit shots are used in total?

### C. Challenge

10. Design a simple QML pipeline and label each component: data, encoding, quantum model, measurement, loss, and optimizer.
11. Compare a quantum kernel model with a variational classifier. Which parts are trained in each case?
12. Give an example of a learning problem where the target is a quantum object rather than a classical label.

## 16. Key takeaways

- QML is a broad field, not a single circuit architecture.
- Classical-data QML and quantum-data learning are different settings.
- Encoding, quantum processing, measurement, loss, and optimization are separate components.
- PQC, VQC, VQA, QNN, and QML should not be used as synonyms.
- Expressivity, trainability, and generalization answer different questions.
- Quantum advantage has several possible meanings and should be interpreted carefully.

## References

1. J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
2. M. Schuld and F. Petruccione, *Supervised Learning with Quantum Computers*, Springer, 2018. https://doi.org/10.1007/978-3-319-96424-9
3. M. Cerezo et al., "Challenges and opportunities in quantum machine learning," *Nature Computational Science* 2, 567–576 (2022). https://doi.org/10.1038/s43588-022-00311-3
4. V. Havlíček et al., "Supervised learning with quantum-enhanced feature spaces," *Nature* 567, 209–212 (2019). https://doi.org/10.1038/s41586-019-0980-2
