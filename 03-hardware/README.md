# Quantum Hardware Platforms

A quantum algorithm is an abstract procedure. A hardware platform is the physical system that stores, controls, couples, and measures quantum information.

This section focuses on the engineering translation

```text
abstract qubit / mode
-> physical degree of freedom
-> control mechanism
-> entangling interaction
-> measurement
-> error model
-> scalable architecture.
```

The central principle is

```math
\boxed{
\text{hardware platform}
\neq
\text{computational model}
\neq
\text{algorithm}
}
```

The same circuit algorithm can be implemented on several hardware technologies, but its physical resource cost can differ dramatically.

## Recommended learning path

```text
superconducting circuits
-> trapped ions
-> neutral atoms
-> photonics
-> semiconductor / spin qubits
-> topological approaches
```

The ordering is not a ranking. Each platform optimizes a different set of physical tradeoffs.

## Contents

1. [Superconducting Qubits](01-superconducting-qubits.md)
2. [Trapped-Ion Quantum Computing](02-trapped-ions.md)
3. [Neutral-Atom Quantum Computing](03-neutral-atoms.md)
4. [Photonic Quantum Computing](04-photonics.md)
5. [Semiconductor and Spin Qubits](05-spin-qubits.md)
6. [Topological Approaches](06-topological-approaches.md)

## Common hardware questions

For every platform, ask:

```text
What physical states encode information?
How are single-qubit / single-mode operations driven?
What physical interaction generates entanglement?
How is measurement performed?
What are the dominant errors?
What connectivity is native?
How are qubits moved or routed?
How fast are reset and measurement?
What resources dominate fault tolerance?
```

These questions are often more informative than qubit count alone.

## Platform comparison map

| Platform | Information carrier | Entangling mechanism | Natural connectivity | Major scaling themes |
|---|---|---|---|---|
| Superconducting | nonlinear microwave circuits | couplers / driven circuit interaction | fabricated local graph | cryogenics, crosstalk, calibration, QEC cycles |
| Trapped ions | atomic internal states | collective motional modes | high within modules | motional modes, laser control, shuttling/modules |
| Neutral atoms | atomic internal/Rydberg states | Rydberg interaction/blockade | reconfigurable geometric | loading, rearrangement, loss, optical control |
| Photonics | photons / optical modes | interference + measurement / resource states | optical routing | loss, sources, detectors, multiplexing |
| Spin qubits | electron/nuclear spins | exchange / mediated coupling | dense local arrays | tuning, wiring, materials, shuttling |
| Topological approaches | nonlocal topological/fusion degrees of freedom | braiding / parity operations | architecture dependent | material realization, protected gate set, readout, QEC |

This table is qualitative; it should not be read as a static performance ranking.

## Learning goals

After completing this section, you should be able to:

- distinguish physical from logical qubits,
- explain why real qubits are rarely exact mathematical two-level systems,
- identify native control and entangling mechanisms for major platforms,
- distinguish coherence, gate error, leakage, loss, crosstalk, and readout error,
- explain why connectivity affects compiled circuit depth,
- understand that measurement/reset latency can matter as much as gate time,
- explain the scaling role of cryogenics, optics, wiring, calibration, and fabrication,
- compare routing through SWAPs, ion shuttling, atom rearrangement, and optical interconnects,
- distinguish hardware-native analog dynamics from digitally compiled gates,
- distinguish physical topological protection from topological QEC codes,
- and translate a QML architecture into a platform-specific resource question.

## Error taxonomy

Hardware error should not be summarized only by one gate-fidelity number.

Important categories include:

### Relaxation

Population leaves an excited computational state.

### Dephasing

Relative phase information decays.

### Leakage

Population exits the intended computational subspace.

### Loss / erasure

The physical information carrier disappears or becomes detectably unavailable.

### Coherent control error

A gate systematically overrotates, underrotates, or uses a miscalibrated axis.

### Crosstalk

Operations intended for one subsystem affect another.

### Measurement error

The classical output does not accurately identify the quantum state/observable outcome.

Different platforms have different mixtures of these error channels.

## Hardware resource vector

Instead of reporting only

```math
N_{\mathrm{qubits}},
```

use a vector such as

```math
R_{\mathrm{hw}}
=
(
N,
D_{2q},
t_{2q},
t_{\mathrm{meas}},
t_{\mathrm{reset}},
p_{\mathrm{loss}},
p_{\mathrm{leak}},
\text{connectivity},
\text{control overhead}
).
```

For fault tolerance, add:

```text
code distance
syndrome-cycle time
logical error rate
physical qubits per logical qubit
non-Clifford state/factory cost
classical decoder latency.
```

A meaningful hardware comparison should specify which coordinates dominate the target algorithm.

## Hardware-aware compilation

An abstract circuit

```math
U
=
U_L\cdots U_1
```

must be translated to native operations.

Compilation can change:

- two-qubit gate count,
- depth,
- routing,
- pulse duration,
- crosstalk schedule,
- logical/non-Clifford overhead.

Therefore two hardware platforms can implement the same abstract algorithm with very different physical costs.

## Hardware-aware QML

QML is particularly sensitive to hardware because training repeatedly executes related circuits.

A hardware-aware QML design should ask:

```text
Which gates are native?
Which interactions are cheap?
What is the connectivity?
How expensive is measurement?
Can observables be measured in parallel?
How fast is reset?
Does the platform provide useful analog dynamics?
Can parameter sharing reduce recalibration?
```

A model with slightly fewer parameters can still be much slower if every loss/gradient estimate requires expensive measurement cycles.

## Native-QML opportunities

Different platforms suggest different model families.

### Superconducting

```text
shallow digital PQCs
local dynamic circuits
fast repeated parameterized microwave control.
```

### Trapped ions

```text
long-range Ising/XX feature maps
high-connectivity variational models
analog spin reservoirs.
```

### Neutral atoms

```text
geometric graph embeddings
Rydberg analog feature maps
many-body quantum-data learning.
```

### Photonics

```text
continuous-variable kernels
generative sampling
measurement-based models
quantum communication/distributed learning.
```

### Spin qubits

```text
exchange-native local circuits
symmetry-aware spin models
dense local architectures.
```

### Topological hardware

```text
architectures minimizing expensive unprotected / non-Clifford operations.
```

These are architectural suggestions, not claims of quantum advantage.

## Fair hardware comparison

Do not compare platforms using one isolated metric such as:

```text
qubit count
or
gate speed
or
coherence time.
```

Instead define the workload and measure the resources required to execute it to a target success probability.

A platform with slower gates but better connectivity can beat a faster nearest-neighbor system for one circuit and lose for another.

The workload determines the relevant tradeoff.

## Physical versus logical resources

A near-term experiment may report physical circuit resources directly.

A fault-tolerant algorithm should instead begin with logical resources and then map them to physical overhead:

```text
logical qubits / gates
-> code choice and target failure rate
-> physical qubits
-> syndrome cycles
-> factories
-> wall-clock time.
```

This mapping is architecture dependent.

## Suggested study method

For each platform:

1. Write the physical Hamiltonian/degree of freedom at a conceptual level.
2. Identify the computational subspace.
3. Identify the native one- and two-body controls.
4. Describe the measurement chain from quantum state to classical bit.
5. List dominant physical error mechanisms.
6. Draw the connectivity/routing architecture.
7. Translate one abstract algorithm into native resources.
8. Propose one QML architecture that exploits the native physics rather than ignoring it.

## Core references

Each platform chapter cites primary or review literature specific to its physical implementation. For cross-platform context, useful broad references include:

- M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
- J. Preskill, *Quantum Computing in the NISQ era and beyond*, *Quantum* 2, 79 (2018).
- T. D. Ladd et al., "Quantum computers," *Nature* 464, 45–53 (2010).
