# Learning from Quantum Data

## 1. A fundamentally different QML regime

Many QML discussions begin with classical vectors and ask how to encode them into qubits.

Learning from quantum data starts elsewhere: the input is already a quantum object.

Examples include

```math
\rho,
\qquad
|\psi\rangle,
\qquad
\mathcal E,
\qquad
H,
\qquad
\Upsilon_{k:0},
```

where the last symbol can represent a multi-time quantum process or process tensor.

This setting is often more naturally quantum because converting the input into a complete classical description can itself destroy information or require many experiments.

## 2. Learning objectives

After this chapter, you should be able to:

- classify quantum-data learning tasks by object type,
- distinguish state learning from state tomography,
- compare separate, adaptive, and collective measurements,
- formulate channel and Hamiltonian learning experiments,
- explain why multi-time processes require objects beyond single channels,
- distinguish quantum-processing advantage from classical-transcript baselines,
- identify quantum memory and joint measurement as possible resources,
- and formulate quantum-native learning tasks where classical feature encoding is absent.

## 3. What counts as quantum data?

A datum can be quantum if the learner receives physical access to a system whose relevant information has not yet been irreversibly converted into classical outcomes.

Examples:

### Quantum state

```math
\rho_x.
```

### Quantum channel

```math
\mathcal E_x.
```

### Hamiltonian-generated dynamics

```math
U_x(t)
=
e^{-iH_xt}.
```

### Multi-time process

A process with memory responding to interventions at several times.

The learner's interface to each object must be specified.

## 4. Quantum state classification

Suppose examples are states

```math
\rho_x
```

with labels

```math
y_x.
```

A classifier may perform a POVM

```math
\{E_y\}
```

and predict according to

```math
p(y|x)
=
\mathrm{Tr}(E_y\rho_x).
```

The measurement itself is the classifier.

No classical feature vector is required unless one chooses to create one through measurement.

## 5. State discrimination as supervised learning

For an ensemble

```math
\{p_y,\rho_y\},
```

classification success is

```math
P_{\mathrm{succ}}
=
\sum_y
p_y
\mathrm{Tr}(E_y\rho_y).
```

Optimizing over POVMs gives the best physically allowed classifier for that ensemble.

This is a powerful reminder:

> A QML model can be a learned measurement rather than a learned unitary feature extractor.

## 6. Learning a measurement

A parameterized measurement can be implemented by applying a trainable unitary before a fixed computational-basis measurement:

```math
E_y(\theta)
=
U_\theta^\dagger
|y\rangle\langle y|
U_\theta.
```

More general measurements can use ancillas, channels, and adaptive protocols.

Training then optimizes

```math
\theta
```

for discrimination or another statistical objective.

This reverses the standard assumption that the measurement is fixed and only the circuit is trainable.

## 7. Tomography versus task-specific learning

Quantum state tomography attempts to reconstruct a complete classical estimate

```math
\widehat\rho
\approx
\rho.
```

But many tasks ask only for one property:

```math
f(\rho).
```

Examples:

- phase label,
- fidelity to a reference state,
- local observable,
- entanglement witness,
- energy density.

Learning $f(\rho)$ can require far fewer experiments than learning the full matrix.

Therefore full tomography is often the wrong baseline.

## 8. Observable prediction

Suppose the learner wants

```math
\mu_j
=
\mathrm{Tr}(O_j\rho)
```

for many observables $O_j$.

Possible strategies include:

```text
measure each observable independently
```

or

```text
collect reusable randomized measurement data
-> classical shadow / compressed representation
-> predict many observables later.
```

The appropriate classical baseline should exploit this reuse.

## 9. Separate measurements

Given

```math
\rho^{\otimes N},
```

a separate-measurement protocol applies one measurement to each copy individually.

Measurements can be fixed or adaptively chosen.

The quantum state is classicalized copy by copy, producing a transcript

```math
D
=
(y_1,\ldots,y_N).
```

All later computation can be classical.

## 10. Collective measurements

A collective learner stores multiple copies and performs one joint measurement on

```math
\rho^{\otimes N}.
```

This can access correlations across copies that no fixed product measurement uses directly.

For some inference problems, collective measurements improve copy complexity or constants.

The resource is not merely “having a quantum computer”; it is specifically the ability to retain quantum memory across examples and perform joint measurements.

## 11. Adaptive measurements

An adaptive protocol chooses

```math
M_t
=
\pi(y_1,\ldots,y_{t-1}).
```

The next experiment depends on previous outcomes.

This can improve efficiency when uncertainty is highly nonuniform or when the learner can actively choose informative measurement settings.

Adaptive state learning sits between static measurement and fully collective processing.

## 12. Classicalization boundary

A useful conceptual boundary is

```text
quantum experiment
-> measurement
-> classical transcript.
```

Before this boundary, the learner can manipulate coherence, entanglement, and noncommuting observables.

After it, the information is classical.

A quantum learning advantage may arise because the optimal decision requires processing information **before** this classicalization boundary.

## 13. Learning from experiments

Consider an experiment that prepares an unknown state or process repeatedly.

A classical-data strategy chooses measurements and records outcomes.

A quantum-data strategy may instead route experimental outputs into quantum memory or a quantum processor before final measurement.

For carefully constructed tasks, preserving coherent quantum information can reduce the number of experiments required relative to strategies that immediately convert each experiment to classical data.

This is a sample/experiment advantage, not merely a faster classifier evaluation.

## 14. Why this regime is conceptually attractive

For classical datasets, one must justify why data should be encoded quantum mechanically.

For quantum data, the opposite question appears:

> Why should inherently quantum information be measured and classicalized before learning if the learning task can benefit from coherent processing?

This reverses the burden of justification.

## 15. Quantum channel learning

An unknown channel

```math
\mathcal E
```

can be probed by choosing input states

```math
\rho_j
```

and measurements on outputs

```math
\mathcal E(\rho_j).
```

Tasks include:

- channel discrimination,
- process tomography,
- parameter estimation,
- predicting future outputs,
- property testing.

The experimental design is part of the learner.

## 16. Entangled channel probes

A learner can prepare

```math
\rho_{RA}
```

entangled between a reference $R$ and channel input $A$.

After applying the channel,

```math
\sigma_{RB}
=
(\mathcal I_R\otimes\mathcal E_A)(\rho_{RA}).
```

A joint measurement on $RB$ may distinguish channels better than unentangled probes for some tasks.

Thus entangled ancillas can become an experimental learning resource.

## 17. Adaptive channel learning

With multiple channel uses, the learner can choose later probes based on earlier outcomes.

More general quantum strategies can retain quantum memory between channel calls.

This produces a hierarchy:

```text
parallel independent probes
adaptive classical memory
adaptive quantum memory
general coherent strategies.
```

Different tasks can separate these strategies.

## 18. Hamiltonian learning

Suppose a system evolves according to

```math
U(t)
=
e^{-iHt}.
```

The unknown Hamiltonian might have structure

```math
H(\theta)
=
\sum_j\theta_jP_j.
```

The learning task is to infer parameters

```math
\theta_j
```

from controlled experiments.

This connects QML with system identification and quantum metrology.

## 19. Experiment design for Hamiltonian learning

The learner can choose:

- initial state,
- evolution time,
- control pulses,
- measured observable,
- adaptive next experiment.

The best experiment depends on current uncertainty about $H$.

Therefore Hamiltonian learning is naturally an **active learning** problem rather than a passive fixed-dataset problem.

## 20. Fisher-information viewpoint

For parameter $\theta$, a measurement distribution

```math
p(y|\theta)
```

has classical Fisher information

```math
F(\theta)
=
\sum_y
p(y|\theta)
\left(
\frac{\partial}{\partial\theta}
\log p(y|\theta)
\right)^2.
```

A quantum experiment can choose measurements to approach the quantum Fisher-information limit.

Thus learning architecture can be designed to maximize parameter sensitivity rather than classification accuracy.

## 21. Phase-of-matter learning

Quantum states from many-body systems can be labeled by physical phase.

A model can learn from copies of

```math
\rho(\lambda)
```

or ground states

```math
|\psi(\lambda)\rangle.
```

Useful architectures may exploit:

- locality,
- order parameters,
- symmetries,
- entanglement patterns,
- multiscale structure.

QCNNs are particularly natural in this setting.

## 22. Learning nonlocal properties

Some properties are difficult to infer from a small fixed set of local observables.

A quantum learner can potentially implement a global coherent measurement targeted directly to the property.

The right comparison is then not

```text
quantum classifier vs classical neural network
```

but

```text
coherent joint measurement
vs
best classical-transcript measurement strategy.
```

This is a cleaner information-theoretic comparison.

## 23. Multi-time quantum processes

If a system interacts with an environment possessing memory, one time step cannot be described independently by a fixed channel

```math
\rho_t
\mapsto
\rho_{t+1}.
```

The system response can depend on earlier interventions.

A process tensor or quantum comb describes the multi-time mapping from a sequence of operations to future outputs.

## 24. Why i.i.d. datasets can be the wrong abstraction

Standard ML assumes examples such as

```math
(x_i,y_i)
```

are drawn independently from a distribution.

A quantum process with memory instead produces data where interventions change future system behavior.

The learner's dataset is better thought of as

```text
intervention history
-> quantum response
-> next intervention.
```

This is closer to causal inference, control, and system identification than static classification.

## 25. Quantum comb viewpoint

A quantum comb represents a higher-order process with open slots into which operations can be inserted.

Conceptually:

```text
operation A_1
-> unknown process
-> operation A_2
-> unknown process
-> ...
-> output.
```

Learning such an object means learning how the process responds to interventions, not merely fitting isolated input-output state pairs.

## 26. Process learning and causality

Multi-time learning can ask:

- Does the process have memory?
- Which earlier interventions influence later outputs?
- What is the causal order?
- Can a lower-memory model approximate it?

These questions connect quantum learning to causal structure and open-system theory.

## 27. Quantum memory as a learning resource

Suppose a learner receives quantum examples sequentially.

A classical strategy measures each example immediately and stores classical outcomes.

A quantum strategy can maintain a memory state

```math
\sigma_t
```

updated by

```math
\sigma_{t+1}
=
\mathcal E(\sigma_t\otimes\rho_t).
```

A separation between these strategies would identify quantum memory itself as the resource.

## 28. Measurement incompatibility as structure

Suppose relevant targets depend on several noncommuting observables

```math
O_1,
O_2,
\ldots.
```

No single projective measurement can reveal all of them sharply on one copy.

This incompatibility is not merely an inconvenience; it can define the statistical structure of the learning problem.

A possible research question is whether uncertainty relations can act as an effective regularizer or constrain hypothesis classes in useful ways.

## 29. Learning quantum sufficient statistics

Instead of reconstructing a full quantum state, seek a compressed quantum representation

```math
\rho
\longmapsto
\sigma_Q
```

that preserves all information needed for a downstream task.

This is a quantum analogue of sufficient-statistic learning.

The representation may deliberately have smaller Hilbert-space dimension or restricted observable content.

This connects learning from quantum data with information bottlenecks and resource-aware compression.

## 30. Classical shadows as competitor

For many observable-prediction tasks, a strong competitor is:

```text
randomized quantum measurements
-> classical shadow
-> classical prediction.
```

This baseline uses quantum experiments but no long-lived quantum learning processor.

Therefore a “quantum learner” should often be compared against sophisticated **quantum-measurement + classical-processing** strategies, not purely classical raw-data algorithms.

## 31. Three competitor classes

It is useful to distinguish:

### Purely classical-data learner

Receives an already classical dataset.

### Quantum measurement + classical learner

Can design measurements on the quantum source but stores only classical transcripts.

### Fully quantum learner

Can maintain quantum memory and process multiple quantum examples coherently.

A learning advantage may exist only between the second and third classes.

That is still a meaningful quantum advantage, but it should be named accurately.

## 32. Resource accounting

For quantum-data learning, relevant resources include:

```text
number of state copies
number of channel uses
number of experimental preparations
quantum memory size
coherent storage time
entangled ancillas
measurement settings
classical transcript size
adaptive rounds
circuit depth.
```

Wall-clock runtime alone can obscure the actual scientific bottleneck.

## 33. Common misconceptions

### “Quantum data means tomography is required before learning.”

No. Direct property learning can avoid full reconstruction.

### “A quantum learner should be compared only with a classical computer receiving a classical dataset.”

Often the stronger baseline is a classical learner allowed to choose quantum measurements first.

### “Collective measurements are always necessary for quantum advantage.”

No. Their usefulness is task dependent.

### “Hamiltonian learning is just regression on time-series data.”

Not generally. The learner can actively choose quantum probes, evolution times, and measurements.

### “A non-Markovian quantum process can always be represented by one fixed channel per time step.”

Memory can invalidate that description.

## 34. Research program: preserve quantum data only when needed

A useful task-first workflow is:

1. identify target information;
2. find the best measurement-plus-classical strategy;
3. determine what information that strategy irreversibly loses;
4. ask whether quantum memory or collective processing preserves useful extra information;
5. prove or test a separation under matched copy/experiment budgets.

This is often cleaner than starting from a VQC architecture.

## 35. Exercises

### Conceptual

1. Why is learning a property of $\rho$ potentially much easier than learning $\rho$ itself?
2. Distinguish a quantum measurement + classical learner from a fully quantum learner.
3. Why can an entangled reference help in channel learning?
4. Why are process tensors needed when a system has temporal memory?

### Computational

5. For binary state discrimination with POVM $\{E_0,E_1\}$, write the average success probability for priors $p_0,p_1$.
6. Suppose a Hamiltonian is

```math
H(\theta)=\theta Z.
```

Starting from $|+\rangle$, derive $\langle X(t)\rangle$ and $\langle Y(t)\rangle$ as functions of $\theta t$.
7. For an adaptive experiment with posterior entropy decreasing from 5 bits to 3.5 bits after one measurement, compute the information-gain reward.
8. Write a memory-update channel for a sequential learner receiving one qubit state $\rho_t$ per round.

### Research-oriented

9. Design a task where learning the measurement/POVM is more natural than learning a state-processing circuit.
10. Formulate an experiment comparing immediate classicalization with coherent two-copy processing under the same copy budget.
11. Propose a process-learning task where i.i.d. supervised-learning assumptions fail explicitly.
12. What is the smallest quantum memory dimension that could provide an advantage for a chosen sequential state-learning task?

## 36. Key takeaways

- Learning from quantum data removes the need to justify classical-to-quantum encoding but introduces copy, measurement, and quantum-memory resources.
- The learner may train measurements, channels, experimental policies, or process models rather than only scalar predictors.
- Task-specific learning can be far cheaper than full tomography.
- Separate, adaptive, and collective measurements define different access models.
- Quantum memory can be a candidate learning resource when classicalization loses relevant information.
- Channel, Hamiltonian, and process learning naturally connect QML with metrology, control, and causal inference.
- Strong baselines include classical shadows and optimized quantum-measurement strategies followed by classical processing.

## References

1. H.-Y. Huang et al., "Quantum advantage in learning from experiments," *Science* 376, 1182–1186 (2022). https://doi.org/10.1126/science.abn7293
2. H.-Y. Huang, R. Kueng, and J. Preskill, "Predicting many properties of a quantum system from very few measurements," *Nature Physics* 16, 1050–1057 (2020). https://doi.org/10.1038/s41567-020-0932-7
3. F. A. Pollock et al., "Non-Markovian quantum processes: Complete framework and efficient characterization," *Physical Review A* 97, 012127 (2018). https://doi.org/10.1103/PhysRevA.97.012127
4. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
