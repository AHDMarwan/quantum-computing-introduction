# Quantum Machine Learning

Quantum machine learning (QML) studies learning problems in which quantum information, quantum computation, quantum data, quantum measurement, or quantum access models play an essential role.

This section deliberately avoids defining QML as “a parameterized quantum circuit trained like a neural network.” Variational classifiers are one family inside a much broader field.

The section is organized around a common ontology so that different QML papers can be compared at the level of their actual computational assumptions rather than terminology alone.

## Recommended learning path

```text
What is QML?
-> data access and encoding
-> PQC / VQC / QNN terminology
-> quantum kernels
-> structured architectures
-> generative QML
-> reservoir computing
-> reinforcement learning
-> quantum learning theory
-> learning from quantum data
-> generalization
-> trainability
-> quantum advantage and dequantization
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

## Phase 6 ontology

Every QML method in this repository should be decomposed into the following layers:

```text
1. Task
2. Data type
3. Data-access model
4. Encoding / representation
5. Quantum hypothesis class
6. Trainable objects
7. Measurement / readout
8. Loss / objective
9. Training / optimizer
10. Generalization target
11. Resource accounting
12. Classical / restricted baseline
13. Claimed quantum resource
14. Advantage metric
```

A concise mathematical view is

```math
\boxed{
\text{data}
\xrightarrow{\text{access + encoding}}
\text{quantum representation}
\xrightarrow{\text{model/channel}}
\text{measurement}
\xrightarrow{\text{loss + training}}
\text{learned predictor}
}
```

but each arrow hides a separate resource assumption.

## QML is not one computational model

The field contains several qualitatively different settings.

### Classical data, quantum processing

```math
x
\longrightarrow
\rho(x)
\longrightarrow
\mathcal E_\theta
\longrightarrow
y.
```

Examples include variational classifiers and quantum kernels.

### Quantum data, quantum processing

```math
\rho_x
\longrightarrow
\mathcal E_\theta
\longrightarrow
y.
```

Here the learner can preserve quantum information before measurement.

### Quantum experiment, classical learning

```text
quantum system
-> measurement protocol
-> classical transcript
-> classical learner.
```

This is often a very strong baseline for quantum-data learning.

### Hybrid sequential learning

```text
quantum process
<-> adaptive quantum/classical agent
```

Examples include quantum control, QRL, process learning, and adaptive experiment design.

## Core distinction: classical data versus quantum data

For classical input,

```math
x\in\mathbb R^d,
```

a quantum learner usually pays some data-loading or encoding cost.

For quantum input,

```math
\rho,
```

the relevant alternative may instead be whether to:

```text
measure immediately and classicalize
```

or

```text
preserve quantum information and process coherently.
```

These are fundamentally different advantage questions.

## Core distinction: model versus measurement

A standard variational model emphasizes

```math
U_\theta.
```

But predictions depend jointly on state transformation and measurement:

```math
p_\theta(y|x)
=
\mathrm{Tr}
\left[
E_y
\mathcal E_\theta(\rho_x)
\right].
```

Therefore trainable QML can act on:

```text
state preparation
channel / dynamics
measurement / POVM
adaptive experimental policy
or combinations of these.
```

This broader viewpoint is important for research beyond standard VQCs.

## Phase 6 chapter standard

The chapters are designed as research-oriented lecture notes. Where appropriate they contain:

```text
motivation
-> learning objectives
-> mathematical formulation
-> worked examples
-> access/resource assumptions
-> classical baselines
-> common misconceptions
-> conceptual exercises
-> computational exercises
-> research-oriented exercises
-> key takeaways
```

The research exercises intentionally ask not only “how does this model work?” but also “what resource is actually responsible for any claimed advantage?”

## Learning goals

After completing this section, you should be able to:

- define QML without reducing it to VQCs or QNNs,
- distinguish classical-data and quantum-data learning regimes,
- distinguish data representation from data access,
- compare basis, angle, amplitude, Hamiltonian, and repeated encodings,
- identify hidden state-preparation and QRAM-like assumptions,
- distinguish PQCs, ansätze, VQAs, VQCs, and QNNs,
- explain how measurement affects the induced hypothesis class,
- derive fidelity-based quantum kernels,
- analyze kernel geometry, spectrum, concentration, and shot cost,
- distinguish hard kernel simulation from useful learning advantage,
- explain QCNN convolution, pooling, causal cones, and multiscale inductive bias,
- compare structured quantum models with matched tensor-network, CNN, or graph baselines,
- define Born-machine and adversarial quantum generative models,
- distinguish sampling hardness from generative trainability,
- formulate quantum reservoir dynamics and linear readout,
- distinguish computational memory from physical coherence time,
- formulate variational quantum policies and quantum-environment RL,
- distinguish ordinary interaction from coherent environment access,
- classify learning resources as samples, queries, state copies, memory, communication, or runtime,
- distinguish task-specific property learning from full tomography,
- compare separate, adaptive, and collective quantum measurements,
- formulate state, channel, Hamiltonian, and process-learning problems,
- analyze generalization using effective hypothesis structure rather than Hilbert-space dimension alone,
- test extrapolation across system sizes, Hamiltonians, measurements, and noise,
- diagnose trainability through gradients, Fisher information, data concentration, readout, noise, and shot SNR,
- and evaluate quantum-advantage claims using dequantization, strong baselines, resource ablations, and explicit access assumptions.

## QML family comparison map

| Family | Main quantum object | Usually trained quantum parameters? | Main bottleneck |
|---|---|---:|---|
| Variational QML | PQC / channel | Yes | optimization + shots + trainability |
| Quantum kernels | feature map / overlap | Often no | kernel geometry + $N^2$ entries + precision |
| QCNN / structured QNN | local multiscale channel/circuit | Yes | architecture + trainability + baseline matching |
| Quantum generative models | state/channel sampler | Often yes | training + probability/sample estimation |
| Quantum reservoir computing | fixed quantum dynamics | Usually no internal training | measurement + temporal feature quality |
| Quantum reinforcement learning | policy/value/process interaction | Often | environment interactions + quantum shots |
| Quantum-data learning | states/channels/processes | Task dependent | copies + measurements + quantum memory |
| Quantum learning theory | abstract learner/access model | Not architecture specific | lower bounds + resource separation |

## Paper-audit template

When reading a QML paper, fill in the following before evaluating the headline claim.

```text
Task:
Scientific/application motivation:

Data type:
- classical
- quantum state
- quantum channel
- sequential process

Training data size:
Input dimension / system size:

Access model:
- ordinary samples
- classical queries
- coherent oracle
- QRAM-like access
- quantum-state copies
- channel uses
- adaptive experiments

Encoding / feature map:
Preparation cost:

Quantum model:
- PQC
- channel
- kernel
- measurement
- reservoir
- policy
- other

Number of trainable parameters:
Circuit depth:
Two-qubit gate count:

Measurement/readout:
Shots per estimate:

Loss:
Optimizer:
Number of quantum evaluations during training:

Generalization protocol:
Train/validation/test split:
Number of seeds:
Uncertainty reporting:

Strongest classical baseline:
Matched structural baseline:
Quantum-measurement + classical baseline, if relevant:

Claimed quantum resource:
- coherence
- entanglement
- magic
- quantum memory
- noncommuting data
- collective measurement
- coherent access
- other

Advantage metric:
- runtime
- query
- sample/copy
- communication
- representation
- approximation

Evidence level:
- demonstration
- benchmark
- scaling experiment
- theorem
```

If this template cannot be completed from a paper, its learning/advantage claim is under-specified.

## Evidence hierarchy

A useful hierarchy is

```text
quantum model executes
-> quantum model learns
-> beats selected baseline
-> beats strong matched baselines
-> advantage under explicit resource accounting
-> growing scaling separation
-> theorem under explicit assumptions
-> useful advantage after physical overhead.
```

These levels should not be conflated.

## Dequantization as a standard audit

For any apparent quantum advantage, ask:

```text
Which assumptions make the quantum algorithm fast?
Can a classical learner exploit analogous sampling, low-rank, locality,
or other structure?
What is the first genuinely quantum resource that prevents this?
```

This turns dequantization into a constructive research tool rather than a negative result.

## Resource-destroying ablations

If resource $R$ is claimed to matter, compare the original model with a version where $R$ is selectively destroyed.

Examples:

```text
coherence
-> dephase selected sectors

entanglement
-> restrict to product/local operations

quantum memory
-> measure/classicalize between examples

collective measurement
-> restrict to product measurements

coherent oracle
-> replace with classical sampling interface.
```

A performance collapse under a well-controlled ablation provides evidence of resource necessity.

## The minimal-quantum-primitive research program

A central research question for the repository is

```math
\boxed{
\text{What is the minimal genuinely quantum primitive
required for a learning advantage?}
}
```

Possible primitives include:

```text
coherent data access
noncommuting measurements
quantum memory
collective measurements
entanglement
magic/contextuality
adaptive coherent experiments
open-system dynamics.
```

A clean approach is to define nested learner classes

```math
\mathcal C_0
\subset
\mathcal C_1
\subset
\cdots
\subset
\mathcal C_Q
```

where each class adds one resource, then identify the first inclusion that creates a provable or measurable separation on a useful task.

## Task-first research workflow

Instead of

```text
choose circuit
-> choose dataset
-> optimize
-> look for accuracy gain,
```

prefer

```text
1. choose a meaningful learning task
2. identify the information bottleneck
3. define the strongest restricted/classical learner
4. identify a candidate quantum resource
5. derive or measure what the restricted learner cannot do
6. design the smallest quantum learner using that resource
7. perform resource-destroying ablations
8. study scaling
9. include implementation overhead.
```

This workflow makes novelty and advantage easier to interpret.

## Three questions to ask about every QML model

### Can it represent the target?

```math
\text{expressivity / approximation}
```

### Can it be learned?

```math
\text{trainability / sample complexity / optimization}
```

### Is the quantum implementation actually better?

```math
\text{advantage / dequantization / resources}
```

A complete research result should state which of these questions it answers.

## Suggested study method

For each chapter:

1. Write down the input-access model before the architecture.
2. Derive the model's observable prediction mathematically.
3. Identify what information is accessible to the classical readout.
4. Count training and inference resources separately.
5. Choose the strongest structurally matched classical baseline.
6. Ask whether the claimed quantum resource is necessary or merely present.
7. Complete one research-oriented exercise by formulating a possible theorem or ablation.

## Core references

- J. Biamonte et al., "Quantum machine learning," *Nature* 549, 195–202 (2017). https://doi.org/10.1038/nature23474
- M. Cerezo et al., "Challenges and opportunities in quantum machine learning," *Nature Computational Science* 2, 567–576 (2022). https://doi.org/10.1038/s43588-022-00311-3
- H.-Y. Huang et al., "Power of data in quantum machine learning," *Nature Communications* 12, 2631 (2021). https://doi.org/10.1038/s41467-021-22539-9
- H.-Y. Huang et al., "Quantum advantage in learning from experiments," *Science* 376, 1182–1186 (2022). https://doi.org/10.1126/science.abn7293
- E. Tang, "A quantum-inspired classical algorithm for recommendation systems," *Proceedings of STOC* (2019). https://doi.org/10.1145/3313276.3316310
