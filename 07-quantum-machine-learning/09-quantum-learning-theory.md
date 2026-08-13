# Quantum Learning Theory

## 1. What learning theory contributes to QML

Quantum learning theory asks what can or cannot be learned under explicit information-access and resource assumptions.

It is not primarily a catalogue of circuit architectures.

A theoretical learning problem should specify

```math
\boxed{
\text{task}
+
\text{access model}
+
\text{success criterion}
+
\text{resource measure}
}
```

and, for an advantage claim, a comparison class or competitor.

This framework is the cleanest way to separate genuine learning advantage from implementation details.

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish sample, query, copy, runtime, memory, and communication complexity,
- explain PAC-style learning at a high level,
- distinguish classical examples from coherent quantum examples,
- identify quantum-state copies as a statistical resource,
- explain why lower bounds are essential to advantage claims,
- distinguish tomography from property prediction,
- explain the role of collective measurements,
- understand classical shadows as an example of task-specific compression of measurement data,
- and formulate a quantum learning theorem with explicit assumptions.

## 3. Classical PAC-learning template

Let $\mathcal C$ be a concept class and let $D$ be a distribution over inputs.

A learner receives examples

```math
(x,c(x))
```

with

```math
x\sim D.
```

The goal is to output hypothesis $h$ such that, with probability at least

```math
1-\delta,
```

the population error satisfies

```math
\Pr_{x\sim D}[h(x)\neq c(x)]
\le
\epsilon.
```

The sample complexity asks how many labeled examples are needed as a function of

```math
\epsilon,
\delta,
\text{and class complexity}.
```

## 4. Sample complexity versus computational complexity

A hypothesis class can be statistically learnable with few examples while computationally difficult to train.

Conversely, a model may be fast to optimize once enough data are available but require many examples to generalize.

Thus

```math
\text{sample complexity}
\neq
\text{runtime complexity}.
```

Quantum learning can improve one without improving the other.

## 5. Query complexity

In a query model, the learner interacts with an oracle rather than receiving a fixed i.i.d. sample set.

Possible oracles include:

- membership queries,
- value queries,
- phase oracles,
- coherent superposition queries.

The number of oracle uses is the query complexity.

As in quantum algorithms, a query speedup does not automatically imply an end-to-end runtime speedup if oracle implementation is expensive.

## 6. Quantum examples

A coherent labeled example can be represented as

```math
|\psi_c\rangle
=
\sum_x
\sqrt{D(x)}
|x,c(x)\rangle.
```

This provides a superposition of labeled examples in one quantum state.

It is a stronger interface than receiving one classical pair $(x,c(x))$ at a time.

Therefore comparisons must distinguish:

```text
classical sample access
from
coherent quantum-example access.
```

## 7. Access-model fairness

Suppose a quantum learner uses

```math
|\psi_c\rangle
```

while the classical learner receives ordinary examples.

A speedup may arise because the quantum learner has stronger access, because it processes that access quantum mechanically, or both.

A rigorous result should make the source explicit.

This is not a flaw in oracle-model theory; it is a requirement for interpreting what the theorem means physically.

## 8. Quantum data as examples

In a quantum-data learning problem, the examples themselves may be states

```math
\rho_x.
```

The learner receives one or more copies.

The statistical resource is then often

```math
N
=
\text{number of copies / experiments}.
```

This resource has no exact classical analogue because one unknown quantum state cannot be copied arbitrarily.

## 9. Copy complexity

Suppose the learner receives

```math
\rho^{\otimes N}.
```

A task may ask for an estimator $\widehat f$ satisfying

```math
|\widehat f-f(\rho)|
\le
\epsilon
```

with probability at least

```math
1-\delta.
```

The minimum required $N$ is the copy complexity.

This is a natural notion for tomography, property estimation, discrimination, and learning from experiments.

## 10. Separate versus collective measurements

A learner can measure each copy independently:

```math
\rho
\xrightarrow{M_1}
y_1,
\quad
\rho
\xrightarrow{M_2}
y_2,
\quad\ldots
```

or store multiple copies and perform a collective measurement on

```math
\rho^{\otimes N}.
```

Collective measurements can be statistically stronger for some tasks.

Thus quantum memory and joint measurement capability can become learning resources.

## 11. Adaptive measurements

Between copies, a learner may choose the next measurement based on previous outcomes:

```math
M_t
=
\pi(y_1,\ldots,y_{t-1}).
```

This creates an active learning or experimental-design problem.

The hierarchy

```text
fixed separate measurements
< adaptive separate measurements
< collective measurements
```

can matter for specific inference tasks, though the exact ordering of power is task dependent.

## 12. Full tomography is often the wrong baseline

Quantum state tomography attempts to reconstruct a complete classical description of an unknown state.

For an arbitrary $n$-qubit state, the density matrix contains exponentially many parameters.

But many learning tasks require only selected properties, not the full state.

Therefore comparing a quantum learner only against full tomography can dramatically overstate the classical/measurement burden.

The correct baseline should solve the same prediction task directly.

## 13. Property prediction

Suppose the goal is to predict expectation values

```math
\mathrm{Tr}(O_j\rho)
```

for observables

```math
O_1,\ldots,O_M.
```

The learner need not reconstruct every entry of $\rho$.

This distinction can reduce sample complexity substantially.

It illustrates a broad learning principle:

```math
\text{learn the target statistic}
\text{ rather than reconstructing the entire generator}.
```

## 14. Classical shadows

Classical-shadow methods perform randomized measurements and construct a compact classical representation from which many observables can later be predicted.

In suitable settings, the number of measurements can scale only logarithmically with the number $M$ of target observables, multiplied by a task-dependent shadow norm or variance factor.

The key lesson is not one universal formula, but:

> One measurement dataset can support many later predictions without full tomography.

This makes classical shadows an important baseline for quantum-data QML claims.

## 15. Why classical shadows are conceptually important

Suppose a proposed quantum learner predicts thousands of observables from a quantum state.

The naive classical baseline might perform tomography first.

A stronger baseline asks whether one can measure the quantum system efficiently once, store a classical shadow, and answer all required predictions later.

This can eliminate an apparent quantum-memory advantage in some regimes.

## 16. State discrimination

Suppose a state is drawn from ensemble

```math
\{p_x,\rho_x\}.
```

The learner must infer $x$.

For a POVM $\{E_x\}$, success probability is

```math
P_{\mathrm{succ}}
=
\sum_x
p_x
\mathrm{Tr}(E_x\rho_x).
```

Optimizing over measurements is itself a learning/inference problem.

This is a fundamental example where the hypothesis object is a measurement rather than a circuit mapping classical features to labels.

## 17. Binary discrimination

For two states with priors $p_0,p_1$, optimal discrimination is governed by the trace norm of

```math
p_0\rho_0-p_1\rho_1.
```

This provides an information-theoretic limit independent of any particular QNN architecture.

Such optimal bounds are useful because they separate **fundamental statistical difficulty** from algorithm design.

## 18. Learning channels

Instead of copies of a state, the learner may query an unknown channel

```math
\mathcal E.
```

Resources include:

- number of channel uses,
- entangled ancillas,
- adaptivity,
- coherent memory across queries.

The learning task might estimate:

- a channel parameter,
- a property,
- future outputs,
- which channel from a finite family is present.

## 19. Quantum query strategies for channels

A general experiment can choose an input state $\rho_{RA}$ entangled with a reference $R$, apply the unknown channel to $A$, and measure the output:

```math
(\mathcal I_R\otimes\mathcal E_A)(\rho_{RA}).
```

Entangled probes can improve distinguishability for some channel tasks.

Thus ancilla entanglement is an access resource, not merely an architectural decoration.

## 20. Learning theory and lower bounds

An algorithmic upper bound says:

```math
N
\le
f(n,\epsilon,\delta).
```

A lower bound says no learner in a specified model can do better than

```math
N
\ge
g(n,\epsilon,\delta).
```

A genuine asymptotic advantage is strongest when both sides are known and separated.

Without a classical lower bound, “no faster classical method is known” is weaker evidence.

## 21. Information-theoretic lower bounds

Lower bounds can be derived using tools such as:

- distinguishability,
- packing arguments,
- Fano-type inequalities,
- Holevo information,
- data processing,
- quantum hypothesis testing.

The common strategy is to construct many possible targets that are difficult to distinguish with too little information.

## 22. Computational lower bounds

Sometimes sample information is sufficient, but processing it efficiently is believed hard.

Then a learning separation may rely on complexity assumptions rather than pure information theory.

One must distinguish:

```text
information-theoretic impossibility
```

from

```text
computational hardness assumption.
```

These support different strengths of theorem.

## 23. PAC learning of quantum models

A quantum model can still be analyzed through hypothesis-class complexity.

For example, if a parameterized model has controlled effective capacity, one can derive bounds relating training-set size to generalization error.

The Hilbert-space dimension alone does not determine this capacity.

Relevant structure can include:

- number of trainable gates,
- norm constraints,
- measurement family,
- circuit locality,
- effective dimension.

## 24. Online learning

In online learning, examples arrive sequentially and the learner predicts before observing the correct target.

Performance is measured through regret:

```math
\mathrm{Regret}_T
=
\sum_{t=1}^{T}\ell_t(\theta_t)
-
\min_\theta
\sum_{t=1}^{T}\ell_t(\theta).
```

Quantum online learning can study quantum examples, quantum memory, or quantum decision strategies.

This connects naturally to adaptive quantum experiments and control.

## 25. Communication complexity

In distributed learning, the bottleneck may be information exchange rather than local sample count.

A quantum protocol might reduce transmitted bits/qubits or use shared entanglement.

Thus learning theory can study

```math
C_{\mathrm{comm}}
```

as the primary resource.

This is relevant to distributed quantum sensing and federated quantum-data settings.

## 26. Memory complexity

A learner may be restricted in how much information it stores between examples.

Quantum memory can preserve coherence across examples, while a classical learner may store only measurement transcripts.

A learning advantage can therefore be formulated as a memory-resource separation:

```text
small quantum memory
vs
larger classical memory / more samples.
```

Such claims require careful model specification.

## 27. The power of data

A function that is hard to compute from its microscopic physical definition can become easy to predict once labeled examples are available.

This is fundamental to learning theory.

Therefore

```math
\text{simulation hardness}
\not\Rightarrow
\text{learning hardness}.
```

A QML advantage theorem must account for what information training data reveal to the classical learner.

## 28. Cryptographic learning separations

Some provable quantum learning advantages are constructed using cryptographic assumptions or concept classes designed around quantum-accessible structure.

These are theoretically valuable because they establish clean separations.

But they should be distinguished from physically motivated learning tasks in chemistry, materials, sensing, or experiment analysis.

The strength of a theorem and the practical naturalness of a task are separate dimensions.

## 29. The theorem-writing template

A clean learning theorem should look conceptually like:

```text
For task family T_n,
under access model A_Q,
a quantum learner achieves error <= epsilon
with resource Q(n,epsilon,delta).

Every learner in competitor model A_C
requires resource C(n,epsilon,delta),
subject to assumptions X.
```

Then compare

```math
Q(n,\epsilon,\delta)
```

and

```math
C(n,\epsilon,\delta).
```

Without these details, “quantum learning advantage” is not mathematically complete.

## 30. Common misconceptions

### “Fewer qubits means lower sample complexity.”

No. Model storage and statistical information are different resources.

### “Tomography is the classical baseline for every quantum-state learning task.”

No. Task-specific measurement schemes and classical shadows can be much stronger.

### “A quantum query is equivalent to one classical sample.”

Not generally. The access interfaces differ.

### “Quantum advantage means runtime advantage.”

It may instead concern queries, copies, communication, or memory.

### “An upper bound for a quantum learner proves advantage.”

Not without a relevant lower bound or strong comparison for classical learners.

## 31. Exercises

### Conceptual

1. Distinguish sample complexity from query complexity.
2. Why is coherent labeled-example access stronger than ordinary i.i.d. examples?
3. Why is full tomography often an unfair baseline for property prediction?
4. What does a lower bound add to an advantage claim?

### Computational

5. Write the PAC success condition for error $\epsilon$ and confidence $1-\delta$.
6. Suppose a procedure estimates $M$ observables separately with $N$ shots each. Compare its naive measurement count with a hypothetical shadow procedure scaling logarithmically in $M$ times a fixed variance factor.
7. For two equiprobable states, express the binary discrimination objective using a two-outcome POVM.
8. Given regret values over $T$ rounds, write the average regret and state the desired asymptotic behavior.

### Research-oriented

9. Take a QML advantage claim and classify whether its resource is runtime, queries, samples, copies, memory, or communication.
10. Design a quantum-data learning task where collective measurement is the candidate resource.
11. Formulate a classical-shadow baseline for a proposed quantum observable-prediction learner.
12. Write a theorem statement for the question: “What is the minimum genuinely quantum primitive required for learning advantage?”

## 32. Key takeaways

- Quantum learning theory studies the fundamental resources of learning, not one architecture.
- Access models must be specified explicitly because coherent quantum examples can be stronger than classical samples.
- Quantum-state copies, channel uses, memory, and communication can all be learning resources.
- Task-specific prediction can be dramatically easier than full tomography.
- Classical shadows are an important example of powerful classical post-measurement representations.
- Lower bounds distinguish fundamental separations from merely good algorithms.
- Simulation hardness and learning hardness are different notions.
- The cleanest advantage statements specify task, access, success, resource, competitor, and assumptions.

## References

1. S. Arunachalam and R. de Wolf, "Guest Column: A Survey of Quantum Learning Theory," *SIGACT News* 48, 41–67 (2017). https://doi.org/10.1145/3106700.3106710
2. H.-Y. Huang, R. Kueng, and J. Preskill, "Predicting many properties of a quantum system from very few measurements," *Nature Physics* 16, 1050–1057 (2020). https://doi.org/10.1038/s41567-020-0932-7
3. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
