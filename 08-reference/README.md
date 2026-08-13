# Reference

This section provides the shared vocabulary, notation, and sources used throughout the repository.

It is intended to prevent three common problems in technical notes:

```text
notation drifting between chapters
terminology being used inconsistently
references being duplicated without a stable core bibliography
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
- adiabatic and annealing variables,
- continuous-variable systems,
- QML models and learning theory,
- quantum error correction.

Individual chapters may introduce local notation, but they should define it when it first appears.

## Terminology map

[terminology-map.md](terminology-map.md) separates conceptual levels such as

```text
hardware
!=
computational model
!=
PQC / channel / measurement
!=
ansatz / candidate family
!=
VQA / learning algorithm
!=
classification / optimization / generation / control task
```

It also records the repository conventions for ambiguous acronyms such as VQC and QNN.

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
resource monotone
```

The glossary is concise by design. The main chapters contain the full explanations.

## Bibliography

[bibliography.md](bibliography.md) collects textbooks, foundational papers, and major reviews grouped by subject:

```text
quantum computing
computational models
VQAs
QIT / QEC
QML
hardware platforms
```

Chapter-level references are usually the best starting point when you want to learn one topic in more depth.

## How to use this section while studying

A simple workflow is:

```text
1. check notation when a symbol is unfamiliar
2. check the terminology map when two acronyms seem to overlap
3. use the glossary for a quick definition
4. return to the chapter for the full explanation
5. use the bibliography when you want a deeper textbook or primary source
```

This reference section is meant to support the learning path, not replace the chapters themselves.

## Repository-wide mathematical formatting

For GitHub compatibility, this repository uses:

```text
inline math: $...$
display math: fenced ```math blocks
```

Legacy `\(...\)`, `\[...\]`, and standalone `$$` display delimiters are intentionally avoided.
