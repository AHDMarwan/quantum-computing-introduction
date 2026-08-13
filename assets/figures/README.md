# Educational Figures

This directory contains lightweight SVG figures used to support the educational chapters in this repository. Some figures originate from Plotly prototypes and are then simplified or optimized for reliable rendering on GitHub.

The goal is explanatory rather than decorative: a figure is included when geometry, state-space structure, composition, or taxonomy is easier to understand visually than from prose alone.

## Foundations

### Bloch sphere: pure qubit state

![Bloch sphere with a pure qubit state](bloch-sphere-state.svg)

A pure qubit is represented by a unit Bloch vector. Its Cartesian coordinates are the expectation values of the Pauli observables $X$, $Y$, and $Z$.

Best read with [The Bloch Sphere](../../01-foundations/04-bloch-sphere.md).

### Bloch ball: pure and mixed states

![Bloch ball showing pure and mixed states](bloch-ball-pure-mixed.svg)

Pure one-qubit states lie on the surface of the Bloch sphere. Mixed states lie inside the Bloch ball, and the maximally mixed state $I/2$ sits at the origin.

Best read with [The Bloch Sphere](../../01-foundations/04-bloch-sphere.md) and [Density Matrices and Mixed States](../../01-foundations/07-density-matrices.md).

### Measurement axes

![Measurement directions on the Bloch sphere](measurement-bases-bloch.svg)

A projective qubit measurement can be viewed geometrically as choosing an axis. The angle between the state vector and the measurement axis controls the outcome probabilities.

Best read with [The Bloch Sphere](../../01-foundations/04-bloch-sphere.md) and [Measurements and POVMs](../../01-foundations/08-measurements-and-povms.md).

### Two-qubit tensor-product basis

![Two-qubit computational basis](tensor-product-basis.svg)

The tensor product of two two-dimensional qubit spaces produces a four-dimensional joint state space with computational basis $|00\rangle$, $|01\rangle$, $|10\rangle$, and $|11\rangle$.

Best read with [Composite Systems and Tensor Products](../../01-foundations/05-composite-systems.md).

## Quantum machine learning

### QML taxonomy

![Taxonomy of major quantum machine learning families](qml-taxonomy.svg)

Quantum machine learning is a broad field. Variational QML is one branch alongside quantum kernels, structured models, generative methods, reservoir computing, reinforcement learning, quantum-data learning, and quantum learning theory.

Best read with [Quantum Machine Learning](../../07-quantum-machine-learning/README.md).

### Classical-data QML versus quantum-data learning

![Classical-data QML compared with quantum-data learning](qml-classical-vs-quantum-data.svg)

Classical-data QML begins with classical information that must be encoded into a quantum representation. Quantum-data learning begins with a state, channel, Hamiltonian, or process that is already quantum.

Best read with [What Is Quantum Machine Learning?](../../07-quantum-machine-learning/01-what-is-qml.md).

## Figure policy

A figure is added only after the corresponding asset exists in this directory. This keeps the visual index free of broken image links.

Static SVGs are preferred for the GitHub edition because they remain sharp at different zoom levels and do not require JavaScript. Interactive figures can be added later in a web edition without changing the chapter structure.
