# Photonic Quantum Computing

## 1. Quantum information carried by light

Photonic quantum computing uses photons and optical modes to encode and process quantum information.

Photons interact weakly with the environment, making them excellent carriers for communication. The same weak interaction makes deterministic two-photon gates difficult, motivating architectures based on linear optics, measurement, entangled resource states, multiplexing, and measurement-based computation.

## 2. Learning objectives

After this chapter, you should be able to:

- distinguish discrete-variable and continuous-variable photonic encodings,
- explain single-rail, dual-rail, polarization, time-bin, and bosonic-mode viewpoints,
- describe beam splitters and phase shifters as linear-optical primitives,
- explain why measurement-induced nonlinearities are important,
- identify photon source, loss, indistinguishability, detector, and switching requirements,
- explain photonic cluster-state and fusion-based architectures,
- connect photonics with CV computation and boson sampling,
- and identify photonic advantages and bottlenecks for QML.

## 3. Photonic encodings

Quantum information can be encoded in several optical degrees of freedom.

### Polarization

```math
|0\rangle
=|H\rangle,
\qquad
|1\rangle
=|V\rangle.
```

### Dual rail

One photon occupies one of two modes:

```math
|0_L\rangle
=|1,0\rangle,
```

```math
|1_L\rangle
=|0,1\rangle.
```

### Time bin

Logical states occupy different temporal modes.

### Continuous variable

Information is encoded in optical quadratures

```math
\hat x,
\hat p.
```

These encodings lead to different hardware and error models.

## 4. Linear optics

Passive linear-optical transformations mix optical modes while preserving total photon number.

At the mode-operator level,

```math
\hat a_i^\dagger
\mapsto
\sum_jU_{ij}\hat a_j^\dagger
```

for unitary matrix $U$.

Beam splitters and phase shifters generate arbitrary passive interferometers.

## 5. Beam splitter

A two-mode beam splitter transforms

```math
\begin{pmatrix}
\hat a_1\\
\hat a_2
\end{pmatrix}
\mapsto
\begin{pmatrix}
t&r\\
-r^*&t^*
\end{pmatrix}
\begin{pmatrix}
\hat a_1\\
\hat a_2
\end{pmatrix},
```

with

```math
|t|^2+|r|^2=1.
```

Two-photon interference at a beam splitter is a key primitive for photonic entanglement generation and measurement.

## 6. Hong–Ou–Mandel interference

Two indistinguishable photons arriving simultaneously at a balanced beam splitter interfere so that they preferentially exit together rather than one through each output.

This effect depends strongly on photon indistinguishability in:

- arrival time,
- frequency,
- polarization,
- spatial mode.

It is a standard diagnostic of photonic source quality.

## 7. Phase shifters

A phase shift on mode $j$ acts as

```math
\hat a_j^\dagger
\mapsto
 e^{i\phi}\hat a_j^\dagger.
```

Integrated photonics can implement programmable interferometers using meshes of beam splitters and phase shifters.

These optical networks naturally implement matrix transformations relevant to sampling, kernels, and quantum linear optics.

## 8. Why deterministic entangling gates are hard

Photons do not naturally interact strongly with one another in ordinary linear optical materials.

A direct deterministic controlled gate therefore requires strong nonlinear interaction or an alternative architecture.

Linear-optical quantum computing instead exploits:

```text
ancilla photons
+ interference
+ measurement
+ feed-forward.
```

Measurement induces an effective nonlinearity probabilistically.

## 9. KLM principle

The Knill–Laflamme–Milburn approach showed that scalable quantum computation is possible with linear optics, single-photon sources, photodetection, and feed-forward, using measurement-induced gates and teleportation techniques.

The price is substantial ancilla and probabilistic-gate overhead.

This result established linear optics as a universal quantum-computing route despite weak direct photon-photon interactions.

## 10. Measurement-based photonics

A different strategy prepares a large entangled photonic cluster state and performs computation through adaptive measurements.

This shifts complexity from repeated deterministic gates to:

- resource-state generation,
- probabilistic entangling/fusion operations,
- multiplexing,
- feed-forward,
- loss tolerance.

Photonic hardware is therefore closely connected to MBQC.

## 11. Fusion operations

Fusion measurements probabilistically connect smaller entangled photonic resource states into larger graph states.

If fusion fails, the failure can often be heralded by detector outcomes.

Architectures can use multiplexing and graph redundancy so enough successful fusions remain to support computation.

The probability of success becomes a resource-planning parameter.

## 12. Photon sources

Scalable photonic computing needs high-quality sources producing photons that are:

```text
indistinguishable
pure
synchronized
available at high probability.
```

Source technologies include spontaneous nonlinear-optical generation and solid-state emitters.

Probabilistic sources often require multiplexing and heralding.

## 13. Heralding

A heralded source uses one detection event to indicate that a desired photon has been generated elsewhere.

Heralding converts uncertainty into a known success/failure flag.

But detector inefficiency and multiplexing overhead reduce effective source rate.

A logical circuit diagram with “single-photon input” hides this source-preparation infrastructure.

## 14. Indistinguishability

Interference quality depends on photons occupying the same spatiotemporal/spectral mode.

Partial distinguishability leaves which-path information and reduces interference visibility.

This is a coherent error source with direct impact on multi-photon sampling distributions.

## 15. Photon loss

Loss can occur in:

- sources,
- waveguides,
- switches,
- couplers,
- detectors.

If each stage has transmission $\eta_j$, total transmission scales multiplicatively:

```math
\eta_{\mathrm{tot}}
=
\prod_j\eta_j.
```

For many photons and deep optical networks, even small per-component loss becomes severe.

Loss tolerance is therefore a central scaling challenge.

## 16. Detectors

Photonic computation can require detectors that distinguish:

```text
no photon
one photon
multiple photons.
```

Important properties include:

- efficiency,
- dark-count rate,
- timing resolution,
- photon-number resolution,
- recovery time.

Detector performance directly determines gate, fusion, and readout fidelity.

## 17. Feed-forward

Measurement-based photonic computation needs rapid classical processing to choose future optical settings based on detector outcomes.

The optical signal may need to be delayed while the controller computes corrections.

This creates a system-level timing constraint connecting:

```text
detector latency
classical electronics
optical delay
switching speed.
```

## 18. Integrated photonics

Waveguides, interferometers, phase shifters, sources, and detectors can be integrated on photonic chips.

Integration improves stability and scaling density compared with bulk optics.

However, large-scale systems still require low-loss packaging, routing, sources, detectors, and control electronics.

## 19. Boson sampling

Boson sampling injects nonclassical photons into a linear interferometer and samples output photon-number patterns.

Its significance is computational-complexity based: certain sampling distributions are believed difficult for classical computation under specified assumptions.

Boson sampling is not a universal quantum computer by itself, but it is an important photonic demonstration of specialized sampling complexity.

## 20. Gaussian boson sampling

Gaussian boson sampling uses Gaussian input states such as squeezed vacuum and photon-number-resolving detection.

The output probabilities connect to matrix functions such as hafnians.

It provides another specialized photonic sampling model with applications proposed in graph and molecular problems.

As always, sampling hardness should be distinguished from end-to-end application advantage.

## 21. Continuous-variable photonics

Photonic modes naturally support CV quantum computation.

Gaussian optical operations are experimentally natural:

- displacement,
- squeezing,
- interferometry,
- homodyne measurement.

Universal CV computation additionally requires a suitable non-Gaussian resource.

Thus photonic hardware spans both qubit and continuous-variable computational models.

## 22. Photonic quantum communication

Photons are natural flying qubits for quantum networks.

Fiber and free-space optical channels support:

- QKD,
- remote entanglement,
- modular quantum computing,
- distributed sensing.

This makes photonics especially important as an interconnect technology even for processors whose local memories use matter qubits.

## 23. Photonics and QML

Potential photonic QML roles include:

- CV feature maps,
- linear-optical kernels,
- bosonic generative models,
- quantum sampling models,
- photonic reservoir computing,
- distributed quantum-data learning.

Optical interferometers naturally implement high-dimensional linear transformations, while non-Gaussian resources add harder-to-simulate structure.

## 24. Photonic feature geometry

A coherent-state feature map

```math
x
\mapsto
|\alpha(x)\rangle
```

has overlap

```math
|\langle\alpha|\beta\rangle|^2
=
 e^{-|\alpha-\beta|^2}.
```

Thus a simple optical encoding already induces a Gaussian-like kernel.

To claim genuinely quantum advantage, the model must exploit structure beyond what an equivalent classical kernel can reproduce efficiently.

## 25. Resource vector

Relevant photonic resources include:

```text
number of optical modes
number of photons
source probability
indistinguishability
optical depth
transmission/loss
squeezing level
non-Gaussian resource count
detector efficiency
feed-forward latency
samples/shots.
```

Mode count alone is not a complete resource metric.

## 26. Common misconceptions

### “Photons are immune to decoherence.”

They couple weakly to many environments, but loss and distinguishability errors are major challenges.

### “Linear optics is too simple for universal quantum computation.”

With measurement, ancillas, and feed-forward, universal computation is possible.

### “Boson sampling is a universal quantum computer.”

No. It is a specialized sampling model.

### “Large optical mode count means large useful quantum advantage.”

Only if sources, losses, detection, sampling complexity, and target task all scale favorably.

## 27. Exercises

### Conceptual

1. Why does weak photon-photon interaction motivate measurement-based architectures?
2. Explain why indistinguishability is necessary for multi-photon interference.
3. Why is loss multiplicative across optical depth?
4. Distinguish boson sampling from universal linear-optical quantum computing.

### Computational

5. For component transmission $\eta$ repeated through $L$ identical stages, derive total transmission $\eta^L$.
6. Compute the coherent-state overlap fidelity for amplitudes separated by distance $|\alpha-\beta|$.
7. For $N$ identical probabilistic sources with success probability $p$, compute expected successful emissions before multiplexing.
8. Write the dual-rail logical basis and identify what photon loss does to the code space.

### Research-oriented

9. Design a photonic quantum kernel and identify the strongest classical optical/kernel baseline.
10. Propose a resource-destroying ablation that removes non-Gaussianity while preserving the interferometer.
11. How should source and detector overhead be incorporated into a sampling-advantage benchmark?
12. Design a distributed QML task where photonic communication is a native resource rather than an implementation afterthought.

## 28. Key takeaways

- Photonic quantum computing processes quantum information in photons and optical modes.
- Linear optics provides stable interference but weak direct photon-photon interaction motivates measurement-induced and cluster-state architectures.
- Source quality, indistinguishability, loss, detectors, multiplexing, and feed-forward are central scaling resources.
- Photonics naturally supports both discrete-variable and continuous-variable quantum computing.
- Boson sampling is a specialized complexity-oriented sampling model, not universal computation.
- Photonics is important both for processors and for quantum networking.
- Photonic QML must distinguish genuinely quantum optical resources from classically reproducible interferometric or Gaussian kernels.

## References

1. E. Knill, R. Laflamme, and G. J. Milburn, "A scheme for efficient quantum computation with linear optics," *Nature* 409, 46–52 (2001). https://doi.org/10.1038/35051009
2. P. Kok et al., "Linear optical quantum computing with photonic qubits," *Reviews of Modern Physics* 79, 135–174 (2007). https://doi.org/10.1103/RevModPhys.79.135
3. C. Weedbrook et al., "Gaussian quantum information," *Reviews of Modern Physics* 84, 621–669 (2012). https://doi.org/10.1103/RevModPhys.84.621
