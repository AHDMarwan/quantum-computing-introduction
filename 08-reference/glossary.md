# Glossary

A compact glossary of terms used throughout the repository.

| Term | Meaning |
|---|---|
| **Amplitude** | Complex coefficient associated with a basis component of a quantum state. Probabilities are obtained from squared magnitudes after measurement. |
| **Ansatz** | Chosen family of candidate states or transformations used to approximate a solution. |
| **Barren plateau** | Trainability regime in which gradients concentrate near zero, often with unfavorable scaling in system size. |
| **Bell state** | One of four maximally entangled two-qubit states. |
| **Bloch sphere** | Geometric representation of one-qubit states; pure states lie on the surface and mixed states inside the Bloch ball. |
| **Born rule** | Rule assigning measurement probabilities, e.g. $p(y)=\mathrm{Tr}(E_y\rho)$. |
| **Circuit depth** | Number of sequential gate layers along the longest dependent path in a circuit. |
| **Coherence** | Basis-dependent quantum property associated with off-diagonal density-matrix terms and usable phase relations. |
| **Completely positive (CP)** | A map remains positive even when tensored with an identity map on an arbitrary reference system. |
| **CPTP map** | Completely positive trace-preserving map; the mathematical definition of a deterministic quantum channel. |
| **Density operator** | General representation $\rho$ of a quantum state, including pure and mixed states. |
| **Entanglement** | Nonseparability of a multipartite quantum state. |
| **Entanglement entropy** | Von Neumann entropy of a reduced state of a bipartite pure state. |
| **Feature map** | Transformation mapping classical data into a feature representation; in QML often $x\mapsto\rho(x)$ or $|\phi(x)\rangle$. |
| **Fidelity** | Measure of similarity between quantum states. |
| **Gate model** | Computational model in which algorithms are represented by quantum gates and measurements. |
| **Global phase** | Multiplicative phase $e^{i\gamma}$ common to an entire pure state; it does not affect measurement statistics. |
| **Hamiltonian** | Hermitian operator generating time evolution and representing energy in quantum mechanics. |
| **Hilbert space** | Complex inner-product vector space used as the state space of a quantum system. |
| **Hybrid quantum–classical algorithm** | Algorithm combining quantum execution with classical computation or optimization. |
| **Interference** | Constructive or destructive combination of quantum amplitudes caused by relative phase. |
| **Kraus operators** | Operators $K_j$ representing a quantum channel as $\mathcal E(\rho)=\sum_jK_j\rho K_j^\dagger$. |
| **Logical qubit** | Error-corrected qubit encoded across multiple physical degrees of freedom. |
| **Measurement instrument** | Mathematical object specifying both measurement outcome probabilities and conditional post-measurement states. |
| **MBQC** | Measurement-based quantum computing; computation driven by local measurements on an entangled resource state. |
| **Mixed state** | Quantum state not describable by a single state vector; represented by a density operator with purity below one. |
| **NISQ** | “Noisy Intermediate-Scale Quantum,” a term for noisy pre-fault-tolerant processors of intermediate scale. |
| **Observable** | Hermitian operator associated with a measurable quantity. |
| **Oracle** | Black-box or abstract operation providing specified query access to a function or data source. |
| **Partial trace** | Operation used to obtain the reduced state of a subsystem from a joint state. |
| **Pauli matrices** | $X,Y,Z$, the standard one-qubit Hermitian/unitary operators. |
| **PQC** | Parameterized Quantum Circuit: a circuit $U(\boldsymbol\theta)$ containing free parameters. |
| **POVM** | Positive-operator-valued measure: positive operators $\{E_y\}$ summing to identity. |
| **Pure state** | Quantum state representable by a unit vector $|\psi\rangle$, equivalently a rank-one density operator. |
| **QAOA** | Quantum Approximate Optimization Algorithm, a structured variational algorithm with alternating cost and mixer evolutions. |
| **QEC** | Quantum error correction. |
| **QFT** | Quantum Fourier transform. |
| **QML** | Quantum machine learning, the broad field connecting quantum information processing and learning. |
| **QNN** | Quantum neural network; an overloaded architectural term for trainable quantum learning models. |
| **QPE** | Quantum phase estimation. |
| **Qubit** | Two-level quantum information unit with state space $\mathbb C^2$. |
| **Quantum advantage** | Resource advantage of a quantum method over specified classical competitors under explicit assumptions. |
| **Quantum annealing** | Optimization-oriented quantum process based on evolving an energy landscape, often using Ising/QUBO formulations. |
| **Quantum channel** | CPTP map describing deterministic physical evolution of density operators. |
| **Quantum kernel** | Kernel estimated from quantum feature states or quantum measurements. |
| **Quantum resource theory** | Framework specifying free states, free operations, resource objects, and monotones. |
| **Reduced state** | State of a subsystem obtained by partial trace. |
| **Relative phase** | Phase difference between amplitudes; unlike global phase, it can affect interference. |
| **Schmidt decomposition** | Canonical decomposition of a bipartite pure state into paired orthonormal basis states. |
| **Shot** | One execution-and-measurement sample of a quantum circuit or experiment. |
| **Superposition** | Linear combination of quantum basis states with coherent amplitudes. |
| **Tensor product** | Composition rule for joint quantum systems. |
| **Trace distance** | Operational state distinguishability measure $\frac12\|\rho-\sigma\|_1$. |
| **Transmon** | Superconducting qubit design operated in a regime reducing charge-noise sensitivity. |
| **Unitary** | Operator satisfying $U^\dagger U=I$; represents reversible closed-system evolution. |
| **VQA** | Variational Quantum Algorithm: quantum cost estimation combined with classical parameter optimization. |
| **VQC** | Ambiguous acronym; in this repository preferably Variational Quantum Classifier when classification is intended. |
| **VQE** | Variational Quantum Eigensolver. |
| **Von Neumann entropy** | $S(\rho)=-\mathrm{Tr}(\rho\log\rho)$. |

See [Terminology Map](terminology-map.md) for relationships among PQC, VQA, VQE, QAOA, VQC, QNN, and QML.
