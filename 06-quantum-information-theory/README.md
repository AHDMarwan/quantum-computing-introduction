# Quantum Information Theory

Quantum information theory studies the structure, transformation, communication, and resource content of quantum information. It supplies the language needed to reason rigorously about noise, distinguishability, entanglement, communication, learning from quantum data, and fault tolerance.

This section shifts the perspective from “which circuit solves the task?” to

```text
which states exist?
which transformations are physical?
which information is accessible?
which resources can be converted?
which correlations survive local restrictions?
```

## Recommended learning path

```text
quantum channels
-> entropy and distinguishability
-> entanglement theory
-> general resource theories
-> communication protocols and capacities
-> error correction and fault tolerance
```

## Contents

1. [Quantum Channels](01-quantum-channels.md)
2. [Entropy and Information](02-entropy-and-information.md)
3. [Entanglement Theory](03-entanglement-theory.md)
4. [Quantum Resource Theories](04-resource-theories.md)
5. [Quantum Communication](05-quantum-communication.md)
6. [Quantum Error Correction](06-error-correction.md)

## Core mathematical objects

```math
\boxed{
\text{states }\rho,
\quad
\text{channels }\mathcal E,
\quad
\text{measurements }\{E_y\},
\quad
\text{information measures},
\quad
\text{resources}
}
```

These same objects reappear throughout quantum algorithms and quantum machine learning.

## Phase 5 chapter standard

Each chapter is organized around operational questions rather than definitions alone:

```text
mathematical object
-> physical meaning
-> operational task
-> conversion / distinguishability statement
-> worked example
-> resource interpretation
-> common misconception
-> exercises
-> QML connection
```

The goal is to make quantum information theory usable as a research language.

## Learning goals

After completing this section, you should be able to:

- model general physical dynamics as CPTP quantum channels,
- distinguish positivity from complete positivity,
- use Kraus, Stinespring, and Choi representations,
- model measurements and open-system learning as channels,
- compute von Neumann entropy from state spectra,
- distinguish state entropy from measurement entropy,
- compute conditional entropy and mutual information,
- explain negative quantum conditional entropy,
- use quantum relative entropy and data-processing arguments,
- interpret Holevo information as a limit on accessible classical information,
- characterize pure-state entanglement using Schmidt coefficients,
- distinguish classical correlation, entanglement, and Bell nonlocality,
- use the PPT criterion in the dimensions where it is complete,
- explain LOCC, entanglement monotones, distillation, and formation,
- formulate a generic quantum resource theory,
- distinguish coherence, magic, asymmetry, contextuality, and other resources,
- design resource-destroying ablations for quantum models,
- derive teleportation and superdense coding,
- distinguish classical, quantum, private, and entanglement-assisted channel capacities,
- explain why no-cloning changes network architecture,
- distinguish physical and logical qubits,
- derive syndrome logic in simple stabilizer codes,
- state the Knill–Laflamme condition,
- distinguish error correction, error mitigation, and fault tolerance,
- and understand why logical-resource counts must be translated into physical-resource estimates.

## The operational-question principle

Whenever a quantity is introduced, ask what task gives it meaning.

For example:

| Quantity / structure | Operational question |
|---|---|
| Trace distance | How well can two states be distinguished? |
| Relative entropy | How distinguishable are two hypotheses under information processing? |
| Mutual information | How correlated are two systems? |
| Entanglement entropy | How much pure bipartite entanglement is present? |
| Channel capacity | At what asymptotic rate can a specified kind of information be transmitted? |
| Resource monotone | How much resource cannot be increased by free operations? |
| Code distance | How many physical errors can an encoded logical state tolerate? |

This prevents information-theoretic quantities from becoming purely formal symbols disconnected from tasks.

## A recurring distinction: state, process, measurement

Three layers should remain separate:

```math
\rho
\quad\neq\quad
\mathcal E
\quad\neq\quad
\{E_y\}.
```

A state is what is prepared.

A channel is what happens to the state.

A measurement is how quantum information becomes classical outcomes.

Many QML formulations implicitly fix two of these objects and train only the third. Recognizing this is useful when searching for new model families.

## A recurring distinction: correlation, resource, advantage

These terms should also remain separate:

```text
correlation
!=
resource
!=
computational advantage.
```

For example:

- a state may be entangled but useless for a chosen task;
- a resource may be necessary but not sufficient for speedup;
- a learning advantage may come from direct quantum-data access rather than entanglement itself.

A rigorous argument should identify the operational chain connecting the resource to the task.

## Resource-theoretic audit template

For a claimed quantum resource $R$, ask:

1. What are the free states?
2. What are the free operations?
3. What task becomes possible or easier with $R$?
4. Is $R$ necessary?
5. Is $R$ sufficient?
6. Can a resource-destroying map remove $R$ while preserving other structure?
7. Does performance disappear after that ablation?
8. Can resource amount be related to computational or statistical complexity?

This template is particularly useful in QML research.

## Communication-resource audit

For distributed quantum protocols, count separately:

```text
qubits transmitted
classical bits transmitted
pre-shared entanglement
quantum memory time
network fidelity
number of channel uses.
```

A communication advantage is incomplete if pre-distributed entanglement or quantum-memory cost is treated as free without explanation.

## Fault-tolerant resource audit

For a deep quantum algorithm, distinguish:

```text
logical qubits
logical gates
logical depth
non-Clifford count
code distance
physical qubits
syndrome cycles
magic-state throughput
classical decoder cost.
```

The gap between logical and physical resources is essential when interpreting practical feasibility.

## Why this section is central to QML

Quantum machine learning becomes much broader once it is written in QIT language.

Instead of only

```math
x
\rightarrow
U(x,\theta)
\rightarrow
\langle M\rangle,
```

one can study

```math
\rho_x
\xrightarrow{\mathcal E_\theta}
\sigma_x
\xrightarrow{\{E_y\}}
y,
```

where:

- the input may already be quantum,
- the trainable model may be a channel rather than a unitary,
- the measurement itself may be optimized,
- the learning target may be a state, channel, or process,
- performance may be constrained by accessible information or communication complexity.

This viewpoint opens research directions that do not fit the standard variational-classifier pipeline.

## Suggested study method

For each chapter:

1. Write the object's defining mathematical conditions.
2. Identify its physical interpretation.
3. Work through at least one two-level or two-qubit example.
4. State the operational task associated with the main quantity.
5. Identify which transformations are allowed or free.
6. Ask what information is lost under measurement or noise.
7. Complete the research-oriented exercises with QML in mind.

## Core references

- J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
- M. M. Wilde, *Quantum Information Theory*, Cambridge University Press.
- R. Horodecki et al., "Quantum entanglement," *Reviews of Modern Physics* 81, 865 (2009).
- E. Chitambar and G. Gour, "Quantum resource theories," *Reviews of Modern Physics* 91, 025001 (2019).
- B. M. Terhal, "Quantum error correction for quantum memories," *Reviews of Modern Physics* 87, 307 (2015).
