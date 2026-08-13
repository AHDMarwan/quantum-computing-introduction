# Quantum Machine Learning

Quantum machine learning (QML) studies learning problems in which quantum computation, quantum information, quantum measurements, or quantum data play a significant role.

This section treats QML as a broad field rather than reducing it to “a parameterized quantum circuit trained like a neural network.” Variational classifiers are one important family, but they sit alongside quantum kernels, structured quantum models, generative methods, reservoir computing, reinforcement learning, learning theory, and learning directly from quantum data.

## Recommended learning path

```text
What is QML?
→ data access and encoding
→ PQC / VQC / QNN terminology
→ quantum kernels
→ structured architectures
→ generative QML
→ reservoir computing
→ reinforcement learning
→ quantum learning theory
→ learning from quantum data
→ generalization
→ trainability
→ quantum advantage
```

## Contents

1. [What Is Quantum Machine Learning?](01-what-is-qml.md)
2. [Data Access and Quantum Encoding](02-data-encoding.md)
3. [PQC, VQC, QNN, and Related Terminology](03-pqc-vqc-qnn.md)
4. [Quantum Kernel Methods](04-quantum-kernels.md)
5. [Quantum Convolutional and Structured Architectures](05-qcnn.md)
6. [Quantum Generative Models](06-generative-qml.md)
7. [Quantum Reservoir Computing](07-quantum-reservoir-computing.md)
8. [Quantum Reinforcement Learning](08-quantum-reinforcement-learning.md)
9. [Quantum Learning Theory](09-quantum-learning-theory.md)
10. [Learning from Quantum Data](10-learning-from-quantum-data.md)
11. [Generalization in Quantum Machine Learning](11-generalization.md)
12. [Trainability in Quantum Machine Learning](12-trainability.md)
13. [Quantum Advantage in Learning](13-quantum-advantage.md)

## A useful way to describe a QML method

When two QML methods look similar, the following layers help make the differences clear:

```text
1. learning task
2. data type
3. data-access model
4. encoding / representation
5. quantum model
6. trainable parameters, if any
7. measurement / readout
8. loss or objective
9. training procedure
10. evaluation metric
```

A generic pipeline can be summarized as

```math
\boxed{
\text{data}
\xrightarrow{\text{encoding or direct access}}
\text{quantum representation}
\xrightarrow{\text{quantum processing}}
\text{measurement}
\xrightarrow{\text{classical output}}
\text{prediction or decision}
}
```

Not every QML method contains every step. A quantum kernel, for example, may have no trainable quantum parameters, while a learning problem involving quantum states may not require classical-to-quantum encoding at all.

## Classical data versus quantum data

One of the most important distinctions in QML is the type of input.

### Classical data

A classical feature vector may be encoded as

```math
x
\longmapsto
\rho(x)
```

or

```math
x
\longmapsto
|\phi(x)\rangle.
```

The encoding is part of the model and can strongly affect its behavior.

### Quantum data

The learner may instead receive an actual quantum object such as

```math
\rho,
\qquad
\mathcal E,
\qquad
H.
```

In this setting the goal may be to learn properties of a state, channel, Hamiltonian, or physical process.

These two settings should not be confused: “using a quantum computer on classical data” and “learning directly from quantum data” are different learning problems.

## Main QML families

| Family | Main idea | Typical trainable quantum parameters? |
|---|---|---:|
| Variational QML | Train a parameterized quantum model | Yes |
| Quantum kernels | Use quantum feature states to define similarities | Often no |
| QCNN / structured models | Build locality, symmetry, or hierarchy into the architecture | Usually |
| Quantum generative models | Learn or generate probability distributions or quantum states | Often |
| Quantum reservoir computing | Use fixed quantum dynamics as a feature-generating reservoir | Usually not internally |
| Quantum reinforcement learning | Use quantum models or quantum interactions in sequential decision making | Depends on setting |
| Learning from quantum data | Learn states, channels, Hamiltonians, or processes | Task dependent |
| Quantum learning theory | Study fundamental learning resources and limits | Not architecture specific |

## Terminology to keep separate

QML literature often uses overlapping acronyms. This repository uses the following convention:

```text
PQC = parameterized quantum circuit
Ansatz = candidate family of states or transformations
VQA = variational quantum algorithm / optimization framework
VQC = variational quantum classifier when the task is classification
QNN = broad architecture-dependent term
QML = the full field
```

See [PQC, VQC, QNN, and Related Terminology](03-pqc-vqc-qnn.md) and the [Terminology Map](../08-reference/terminology-map.md).

## What does a learner actually measure?

A common variational QML prediction has the form

```math
p_\theta(y|x)
=
\mathrm{Tr}
\left[
E_y\,\mathcal E_\theta(\rho_x)
\right].
```

This equation is useful because it separates three ideas:

```text
input state
→ quantum transformation
→ measurement
```

The measurement is not merely a final implementation detail: it determines what information becomes available to the classical output.

## Learning goals

After completing this section, you should be able to:

- explain what QML includes and what it does not mean,
- distinguish classical-data and quantum-data learning,
- distinguish data access from data encoding,
- compare basis, angle, amplitude, and repeated encodings,
- explain the difference among PQCs, VQCs, VQAs, and QNNs,
- describe the basic variational QML pipeline,
- derive a fidelity-based quantum kernel,
- explain the role of kernel geometry and kernel concentration,
- describe the structure of QCNNs and other structured quantum models,
- explain the basic idea of quantum generative models,
- describe quantum reservoir computing and its readout,
- distinguish several meanings of quantum reinforcement learning,
- explain what quantum learning theory studies,
- describe learning tasks for states, channels, Hamiltonians, and processes,
- distinguish trainability from expressivity and generalization,
- explain the meaning of barren plateaus and measurement noise in training,
- and interpret a claim of quantum advantage with the correct resource and comparison in mind.

## How the chapters are written

Where appropriate, chapters include:

```text
motivation
→ learning objectives
→ mathematical formulation
→ intuition
→ worked examples
→ comparisons with related methods
→ common misconceptions
→ conceptual exercises
→ computational exercises
→ challenge exercises
→ key takeaways
```

Advanced topics such as dequantization, resource accounting, and lower bounds are included because they help explain what quantum advantage means. They are not required to understand the introductory QML models first.

## A simple checklist when learning a QML model

When you encounter a new model, ask:

1. What is the input?
2. Is the input classical or quantum?
3. How is the information represented?
4. What part of the model is quantum?
5. What parameters are trained?
6. What is measured?
7. What loss or objective is optimized?
8. How is performance evaluated?
9. What classical method is the closest comparison?

This checklist is meant as a learning aid, not as a formal review template.

## Three concepts that should not be confused

### Expressivity

Can the model represent the desired function, state, or distribution?

### Trainability

Can useful parameters be found with a reasonable amount of optimization and measurement effort?

### Generalization

Does the trained model perform well on unseen data or unseen physical instances?

A model can be strong in one of these dimensions and weak in another.

## Quantum advantage as an advanced topic

“Quantum advantage” does not simply mean that one quantum experiment achieves better accuracy than one classical experiment. Depending on the problem, advantage may refer to

```text
runtime
query complexity
sample or copy complexity
memory
communication
representation size
approximation quality
```

The final chapter explains these distinctions and why data loading, measurement cost, and classical baselines matter.

## Suggested study method

For each chapter:

1. Identify the learning problem before looking at the circuit.
2. Write down the input representation mathematically.
3. Identify which quantities are trainable and which are fixed.
4. Follow the quantum state or channel through the model.
5. Write down the measurement that produces the output.
6. Work through the examples and exercises.
7. Compare the method with the previous QML families before moving on.

## Core references

- J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
- M. Schuld and F. Petruccione, *Supervised Learning with Quantum Computers*, Springer, 2018.
- M. Cerezo et al., "Challenges and opportunities in quantum machine learning," *Nature Computational Science* 2, 567–576 (2022). https://doi.org/10.1038/s43588-022-00311-3
- V. Havlíček et al., "Supervised learning with quantum-enhanced feature spaces," *Nature* 567, 209–212 (2019). https://doi.org/10.1038/s41586-019-0980-2
- H.-Y. Huang et al., "Quantum advantage in learning from experiments," *Science* 376, 1182–1186 (2022). https://doi.org/10.1126/science.abn7293
