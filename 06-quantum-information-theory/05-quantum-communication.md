# Quantum Communication

## 1. What quantum communication studies

Quantum communication studies how classical and quantum information can be transmitted, compressed, protected, and transformed when the carriers and channels obey quantum mechanics.

Typical tasks include:

- transmitting an unknown quantum state,
- sending classical messages through quantum channels,
- distributing entanglement,
- quantum key distribution,
- teleportation,
- superdense coding,
- entanglement swapping,
- quantum repeaters,
- distributed quantum computation.

A key lesson is that there is no single “capacity of a quantum channel.” Capacity depends on what resource is being transmitted and what assistance is allowed.

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish classical from quantum information transmission,
- derive the teleportation protocol,
- explain why teleportation does not violate relativity or no-cloning,
- derive superdense coding,
- identify the resource tradeoffs between qubits, classical bits, and entanglement,
- distinguish classical, quantum, private, and entanglement-assisted capacities,
- explain why no-cloning changes network architecture,
- and identify communication complexity as a relevant resource in distributed QML.

## 3. Classical versus quantum messages

A classical communication task sends a classical variable

```math
X\in\mathcal X
```

through a channel and attempts to reconstruct it.

A quantum communication task may instead require transmitting an unknown state

```math
|\psi\rangle
=
\alpha|0\rangle+
\beta|1\rangle
```

while preserving coherence and entanglement with external systems.

This is a stronger requirement than transmitting measurement outcomes of the state.

## 4. Why simply measuring and resending is not enough

Suppose Alice receives an unknown qubit $|\psi\rangle$.

If she measures it in a fixed basis, she obtains only one classical outcome and generally destroys information about incompatible observables.

For example,

```math
|+\rangle
```

and

```math
|-\rangle
```

have identical computational-basis probabilities but different phases.

Therefore an arbitrary unknown quantum state cannot be transmitted perfectly by first converting it into a finite classical description from a single copy.

## 5. Teleportation resources

Quantum teleportation transfers an unknown qubit using:

- one pre-shared Bell pair,
- two classical bits from Alice to Bob,
- local quantum operations and measurements.

It does **not** require physically sending the input qubit itself from Alice to Bob during the protocol.

The shared entangled state is

```math
|\Phi^+\rangle_{AB}
=
\frac{|00\rangle+|11\rangle}{\sqrt2}.
```

Alice holds qubit $A$ and Bob holds qubit $B$.

Alice also receives the unknown state

```math
|\psi\rangle_Q
=
\alpha|0\rangle+
\beta|1\rangle.
```

## 6. Teleportation derivation

The initial three-qubit state is

```math
|\psi\rangle_Q
|\Phi^+\rangle_{AB}.
```

Apply a CNOT from $Q$ to $A$, followed by a Hadamard on $Q$.

The resulting state can be written

```math
\frac12
\Big(
|00\rangle_{QA}|\psi\rangle_B
+
|01\rangle_{QA}X|\psi\rangle_B
+
|10\rangle_{QA}Z|\psi\rangle_B
+
|11\rangle_{QA}XZ|\psi\rangle_B
\Big).
```

Alice measures $Q$ and $A$ in the computational basis.

Her two-bit outcome determines Bob's conditional state.

## 7. Teleportation correction table

| Alice outcome | Bob state before correction | Bob correction |
|---|---|---|
| $00$ | $|\psi\rangle$ | $I$ |
| $01$ | $X|\psi\rangle$ | $X$ |
| $10$ | $Z|\psi\rangle$ | $Z$ |
| $11$ | $XZ|\psi\rangle$ | appropriate Pauli inverse |

After Alice sends the two classical bits, Bob applies the corresponding Pauli correction and recovers

```math
|\psi\rangle.
```

## 8. Why teleportation does not enable faster-than-light communication

Before receiving Alice's classical bits, Bob does not know which correction is required.

Averaging over Alice's possible outcomes, Bob's local state is independent of the unknown message in a way that allows no controllable superluminal signal.

Therefore the protocol requires an ordinary classical communication channel.

The earliest Bob can reconstruct the state is limited by the arrival of those classical bits.

## 9. Why teleportation does not violate no-cloning

Teleportation does not create two copies of $|\psi\rangle$.

Alice's Bell-type measurement irreversibly changes her input system.

After successful completion, the quantum information has moved to Bob; Alice no longer retains the original unknown state.

Thus

```math
\text{teleportation}
\neq
\text{copying}.
```

## 10. Resource interpretation of teleportation

Teleportation implements the resource conversion

```text
1 shared ebit
+ 2 classical bits
-> 1 transmitted qubit state
```

where an **ebit** denotes one maximally entangled qubit pair.

This is an example of quantum information theory treating communication resources algebraically.

## 11. Superdense coding

Superdense coding uses the reverse resource pattern.

Alice and Bob initially share

```math
|\Phi^+\rangle.
```

Alice wants to transmit two classical bits

```math
b_1b_2.
```

She applies one of four local operations to her half of the Bell pair:

```text
00 -> I
01 -> X
10 -> Z
11 -> XZ
```

These operations transform the shared Bell pair into four orthogonal Bell states.

Alice then sends her one qubit to Bob.

Bob performs a Bell-basis measurement and identifies which of the four states was sent.

Thus

```text
1 transmitted qubit
+ 1 shared ebit
-> 2 classical bits.
```

## 12. Bell-state orthogonality

The four Bell states are

```math
|\Phi^\pm\rangle
=
\frac{|00\rangle\pm|11\rangle}{\sqrt2},
```

```math
|\Psi^\pm\rangle
=
\frac{|01\rangle\pm|10\rangle}{\sqrt2}.
```

They are mutually orthogonal, so Bob can distinguish them perfectly with a joint Bell measurement.

This orthogonality is what allows four classical messages to be encoded into the shared two-qubit state using only one transmitted physical qubit after entanglement distribution.

## 13. Teleportation versus dense coding

The two protocols illustrate a resource duality:

```text
Teleportation:
shared entanglement + classical communication
-> quantum communication
```

```text
Dense coding:
shared entanglement + quantum communication
-> enhanced classical communication
```

Entanglement is not itself a signaling channel, but it changes what can be achieved when combined with communication.

## 14. Quantum channels

A noisy communication link is described by a channel

```math
\mathcal N:
\rho
\mapsto
\mathcal N(\rho).
```

Different communication tasks ask how much information can be transmitted reliably using many independent or correlated uses of $\mathcal N$.

The answer depends on whether the message is classical or quantum and what side resources are available.

## 15. Classical capacity

The classical capacity asks for the maximum reliable asymptotic rate of transmitting classical information through a quantum channel.

A sender chooses quantum code states, and the receiver performs quantum measurements to decode classical messages.

The Holevo quantity plays a central role in bounding accessible classical information.

The capacity problem can require regularization across many channel uses because collective coding may outperform naive single-use strategies.

## 16. Quantum capacity

Quantum capacity asks for the asymptotic rate at which arbitrary quantum states, or equivalently entanglement, can be transmitted reliably through a noisy quantum channel.

The challenge is stronger than classical communication because coherence with external reference systems must be preserved.

The relevant information quantity is related to **coherent information**, not simply classical mutual information.

## 17. Private classical capacity

A channel can also be evaluated by how many classical bits can be transmitted securely against an eavesdropper who may access an environment correlated with the channel.

This defines a private classical capacity.

Thus a channel may have different classical, quantum, and private communication capabilities.

## 18. Entanglement-assisted capacity

If sender and receiver share unlimited prior entanglement, the achievable classical communication rate can increase.

The resulting entanglement-assisted capacity has a different operational formula from the unassisted classical capacity.

This illustrates a general principle:

```math
\text{capacity}
=
\text{task}
+
\text{channel}
+
\text{allowed assistance}.
```

There is no context-free single capacity number.

## 19. Erasure intuition

Consider a quantum erasure channel that either transmits a qubit correctly or replaces it with an orthogonal erasure flag known to the receiver.

The explicit flag distinguishes erasure from an unknown Pauli corruption.

This simple model shows how channel structure affects coding strategy and capacity.

Knowing that an error occurred can be much more useful than receiving a corrupted symbol without a flag.

## 20. No-cloning and network architecture

Classical communication networks use repeaters that detect, copy, amplify, and retransmit classical signals.

An unknown quantum state cannot be copied perfectly.

Therefore a quantum network cannot simply place classical amplifiers at intermediate nodes.

Long-distance quantum communication instead uses tools such as:

- entanglement distribution,
- entanglement swapping,
- entanglement purification,
- quantum error correction,
- quantum repeaters.

## 21. Entanglement swapping

Suppose $A$ is entangled with $B$, and $C$ is entangled with $D$.

A suitable joint measurement on $B$ and $C$ can project $A$ and $D$ into an entangled state even though they never directly interacted.

This is entanglement swapping.

It is a core primitive for repeater architectures and distributed quantum networks.

## 22. Quantum repeaters

A long channel may have exponentially poor direct transmission probability with distance.

Quantum repeater ideas divide the distance into shorter segments, distribute entanglement locally, and then connect segments through swapping and purification or error correction.

Relevant resources include:

```text
memory coherence time
entanglement-generation rate
classical signaling delay
fidelity
number of repeater nodes.
```

Network performance is therefore a multi-resource optimization problem.

## 23. Quantum key distribution

Quantum key distribution (QKD) uses quantum communication to establish shared classical secret keys with security grounded in physical/statistical principles rather than only computational hardness assumptions.

Protocols exploit facts such as:

- measurement disturbance,
- no-cloning,
- incompatible measurement bases,
- entanglement correlations.

QKD transmits secret classical key material; it is not the same task as transmitting arbitrary quantum states.

## 24. Communication complexity

Sometimes the main computational resource is not local runtime but the amount of information exchanged between separated parties.

A distributed task can ask:

```text
How many classical or quantum bits must Alice and Bob exchange
in order to compute a joint function?
```

Quantum protocols can reduce communication complexity for some tasks.

This resource perspective is directly relevant to distributed quantum learning.

## 25. Distributed quantum computation

Separate quantum processors can cooperate using:

- transmitted qubits,
- shared entanglement,
- teleportation,
- classical coordination.

A nonlocal logical gate can sometimes be implemented through entanglement-assisted protocols rather than physically moving all quantum data to one processor.

This creates an architecture where communication cost and entanglement generation become central system resources.

## 26. Quantum communication and QML

Distributed QML can involve:

- quantum data stored at separate nodes,
- federated-style learning without centralizing raw quantum states,
- distributed sensing,
- delegated quantum learning,
- privacy-preserving protocols,
- entanglement-assisted inference.

In these settings, the relevant resource may be

```math
\text{communication complexity}
```

rather than only circuit depth or parameter count.

A model that saves local gates but requires enormous entanglement distribution may not be globally efficient.

## 27. Learning quantum states through communication

Suppose several laboratories hold quantum states from different parts of a distributed experiment.

A learning protocol could choose between:

```text
local measurements + classical transcripts
```

and

```text
coherent quantum communication + joint processing.
```

Comparing these models creates natural questions about the value of preserving quantum information before classicalization.

This connects quantum communication directly to learning-from-experiments problems.

## 28. Common misconceptions

### “Teleportation sends information instantaneously.”

No. Bob needs Alice's classical message before recovering the state.

### “Teleportation copies the input state.”

No. The original is destroyed in the protocol.

### “Dense coding sends two classical bits using an isolated single qubit.”

The enhancement consumes pre-shared entanglement.

### “A quantum channel has one capacity.”

Different operational tasks define different capacities.

### “Quantum repeaters can just amplify unknown qubits.”

No-cloning forbids the classical repeater strategy.

## 29. Exercises

### Conceptual

1. Why does teleportation require classical communication even though Alice and Bob share entanglement?
2. Explain why dense coding does not violate the Holevo intuition once pre-shared entanglement is counted.
3. Why must quantum capacity preserve entanglement with a reference system?
4. Why are quantum repeaters fundamentally different from classical signal amplifiers?

### Computational

5. Derive the teleportation identity

```math
|\psi\rangle_Q|\Phi^+\rangle_{AB}
=
\frac12
\sum_{m,n\in\{0,1\}}
|mn\rangle_{QA}
X^nZ^m|\psi\rangle_B
```

up to the chosen Pauli ordering convention.
6. Verify that the four Bell states are orthonormal.
7. Show explicitly how the operations $I,X,Z,XZ$ map $|\Phi^+\rangle$ to the four Bell states up to global phase.
8. If a network distributes one Bell pair per second and a protocol consumes 100 Bell pairs per inference, what is the entanglement-distribution-limited inference rate before other costs?

### Research-oriented

9. Compare a distributed QML protocol based on classical measurement transcripts with one based on coherent quantum communication. What resource metrics should be matched?
10. When could communication complexity be a more meaningful advantage metric than gate complexity?
11. Design a learning task where local classicalization loses information that a joint quantum measurement retains.
12. How should pre-shared entanglement be accounted for in a fair quantum communication advantage claim?

## 30. Key takeaways

- Quantum communication distinguishes transmission of classical information, quantum states, privacy, and entanglement.
- Teleportation consumes one shared ebit and two classical bits to transfer an unknown qubit state.
- Superdense coding consumes shared entanglement to transmit two classical bits with one transmitted qubit.
- Entanglement changes communication capabilities but does not itself transmit signals.
- Quantum channels have different capacities depending on the communication task and allowed assistance.
- No-cloning fundamentally changes network and repeater design.
- In distributed QML, communication and entanglement-distribution costs can be more important than local circuit size.

## References

1. C. H. Bennett et al., "Teleporting an unknown quantum state via dual classical and EPR channels," *Physical Review Letters* 70, 1895 (1993). https://doi.org/10.1103/PhysRevLett.70.1895
2. C. H. Bennett and S. J. Wiesner, "Communication via one- and two-particle operators on Einstein-Podolsky-Rosen states," *Physical Review Letters* 69, 2881 (1992). https://doi.org/10.1103/PhysRevLett.69.2881
3. M. M. Wilde, *Quantum Information Theory*, Cambridge University Press.
4. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
