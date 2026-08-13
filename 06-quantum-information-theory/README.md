# Quantum Information Theory

Quantum information theory studies how quantum information is represented, transformed, measured, communicated, and protected.

This section develops the language of quantum states, channels, entropy, entanglement, communication, resources, and error correction. These ideas are useful throughout quantum computing and later reappear in quantum machine learning.

## Recommended learning path

```text
quantum channels
→ entropy and information
→ entanglement theory
→ resource theories
→ quantum communication
→ quantum error correction
```

## Contents

1. [Quantum Channels](01-quantum-channels.md)
2. [Entropy and Information](02-entropy-and-information.md)
3. [Entanglement Theory](03-entanglement-theory.md)
4. [Quantum Resource Theories](04-resource-theories.md)
5. [Quantum Communication](05-quantum-communication.md)
6. [Quantum Error Correction](06-error-correction.md)

## Core objects

```math
\boxed{
\text{states }\rho,
\quad
\text{channels }\mathcal E,
\quad
\text{measurements }\{E_y\},
\quad
\text{information measures}
}
```

A useful distinction is:

```text
state = what is prepared
channel = how it changes
measurement = how a classical outcome is obtained
```

## Learning goals

After completing this section, you should be able to:

- describe general quantum evolution using CPTP channels,
- use the basic Kraus, Stinespring, and Choi viewpoints,
- compute von Neumann entropy from eigenvalues,
- explain mutual information and conditional entropy,
- understand the basic meaning of quantum relative entropy and Holevo information,
- characterize bipartite pure-state entanglement using Schmidt coefficients,
- distinguish entanglement from ordinary classical correlation,
- explain the idea of LOCC and quantum resource theories,
- derive the logic of teleportation and superdense coding,
- explain what a quantum-channel capacity represents,
- distinguish physical and logical qubits,
- explain syndrome-based quantum error correction,
- and distinguish error correction from fault tolerance and error mitigation.

## Operational meaning

Many quantities in quantum information are easiest to remember by the question they answer.

| Concept | Main question |
|---|---|
| Trace distance | How distinguishable are two states? |
| Mutual information | How correlated are two systems? |
| Entanglement entropy | How much bipartite pure-state entanglement is present? |
| Channel capacity | How much information can be transmitted reliably? |
| Resource monotone | How does a resource behave under allowed operations? |
| Code distance | How much error can an encoded state tolerate? |

## Connection to QML

A general quantum learning pipeline can be written as

```math
\rho_x
\xrightarrow{\mathcal E_\theta}
\sigma_x
\xrightarrow{\{E_y\}}
y.
```

The QIT chapters provide the tools needed to understand each part of this expression: quantum data, quantum transformations, measurements, distinguishability, and information loss.

## Suggested study method

For each chapter:

1. Learn the definition.
2. Translate it into plain language.
3. Work through a one- or two-qubit example.
4. Identify the physical task connected to the concept.
5. Complete the conceptual and computational exercises.
6. Try the challenge exercises after the main examples are comfortable.

## Core references

- J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
- M. M. Wilde, *Quantum Information Theory*, Cambridge University Press.
- R. Horodecki et al., "Quantum entanglement," *Reviews of Modern Physics* 81, 865 (2009).
- E. Chitambar and G. Gour, "Quantum resource theories," *Reviews of Modern Physics* 91, 025001 (2019).
- B. M. Terhal, "Quantum error correction for quantum memories," *Reviews of Modern Physics* 87, 307 (2015).
