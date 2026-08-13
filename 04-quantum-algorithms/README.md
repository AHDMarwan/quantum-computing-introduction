# Quantum Algorithms

This section introduces canonical quantum algorithms and algorithmic primitives. The emphasis is not only on circuit steps but on the **source of the speedup**, the **input-access assumptions**, and the **resource being counted**.

## Contents

1. [Deutsch–Jozsa Algorithm](01-deutsch-jozsa.md)
2. [Grover Search and Amplitude Amplification](02-grover.md)
3. [Quantum Phase Estimation](03-phase-estimation.md)
4. [Shor's Algorithm](04-shor.md)
5. [Quantum Simulation](05-quantum-simulation.md)
6. [Amplitude Estimation](06-amplitude-estimation.md)

## A recurring checklist

For every quantum algorithm, ask:

1. What is the problem?
2. How is the input accessed?
3. What quantum primitive is used?
4. What is the complexity measure?
5. What is the best relevant classical comparison?
6. What assumptions are hidden in oracle or state-preparation access?
7. What changes in a noisy or fault-tolerant implementation?
