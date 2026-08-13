# Reference

This section provides the shared vocabulary, notation, and canonical sources used throughout the repository.

It is intended to prevent three common problems in quantum-computing notes:

```text
notation drifting between chapters
terminology being used at inconsistent conceptual levels
references being duplicated without a stable core bibliography.
```

## Contents

1. [Notation](notation.md)
2. [Terminology Map](terminology-map.md)
3. [Glossary](glossary.md)
4. [Bibliography](bibliography.md)

## Notation

[notation.md](notation.md) defines the default symbols for:

- quantum states and operators,
- channels and measurements,
- information-theoretic quantities,
- circuit resources,
- adiabatic/annealing variables,
- continuous-variable systems,
- QML models and learning theory,
- quantum error correction.

Individual chapters may introduce local notation, but should state it explicitly.

## Terminology map

[terminology-map.md](terminology-map.md) separates conceptual levels such as

```text
hardware
!=
computational model
!=
PQC / channel / measurement
!=
ansatz / hypothesis family
!=
VQA / learning algorithm
!=
classification / optimization / generation / control task.
```

It also defines the repository conventions for ambiguous acronyms such as VQC and QNN.

## Glossary

[glossary.md](glossary.md) is the quick lookup layer for recurring terms such as:

```text
PQC
QAOA
QCNN
QRC
QRL
POVM
quantum channel
collective measurement
classical shadow
dequantization
kernel concentration
trainability
logical qubit
resource monotone.
```

The glossary is concise by design; the chapters contain the full mathematical treatment.

## Bibliography

[bibliography.md](bibliography.md) collects canonical textbooks, foundational papers, and major reviews grouped by subject:

```text
quantum computing
computational models
VQAs
QIT / QEC
QML
hardware platforms.
```

Chapter-level references remain the preferred starting point for a focused literature search.

## Research use

For QML research, combine three files:

```text
Terminology Map
+
QML paper-audit template
+
Bibliography
```

The recommended workflow is:

```text
1. normalize terminology
2. identify task and access model
3. identify the claimed quantum resource
4. identify the strongest competitor
5. trace primary references
6. search recent related work under multiple terminology variants
7. test novelty at the level of mathematical structure, not paper title.
```

The full QML audit template is in [Quantum Machine Learning](../07-quantum-machine-learning/README.md).

## Repository-wide mathematical formatting

For GitHub compatibility, this repository uses:

```text
inline math: $...$
display math: fenced ```math blocks
```

Legacy `\(...\)`, `\[...\]`, and standalone `$$` display delimiters are intentionally avoided.
