# Superconducting Qubits

## 1. Physical principle

Superconducting quantum processors use lithographically fabricated electrical circuits operated at cryogenic temperatures. Josephson junctions provide the nonlinearity required to create addressable anharmonic energy levels.

The dominant modern qubit design is the transmon.

## 2. Transmon Hamiltonian

A simplified transmon Hamiltonian is

$$
H=4E_C(\hat n-n_g)^2-E_J\cos\hat\phi,
$$

where $E_C$ is the charging energy and $E_J$ is the Josephson energy. In the regime $E_J/E_C\gg1$, sensitivity to charge noise is reduced while sufficient anharmonicity remains for qubit control.

## 3. Control and readout

Microwave pulses implement single-qubit rotations. Two-qubit entangling gates are generated through direct or mediated couplings. Readout is commonly dispersive: a qubit shifts the response of a coupled resonator, allowing the qubit state to be inferred from a microwave signal.

## 4. Strengths

Typical strengths include

- fast gate operations,
- compatibility with microfabrication,
- strong microwave control,
- and substantial engineering maturity.

## 5. Challenges

Important challenges include

- decoherence and materials defects,
- frequency crowding,
- crosstalk,
- leakage outside the computational subspace,
- calibration complexity,
- cryogenic wiring and control scaling,
- and error-correction overhead.

## 6. Computational role

Superconducting processors usually implement the gate model, but the physical technology itself is not the model. The same algorithms can in principle be compiled for other hardware.

## References

1. J. Koch et al., "Charge-insensitive qubit design derived from the Cooper pair box," *Phys. Rev. A* 76, 042319 (2007). https://doi.org/10.1103/PhysRevA.76.042319
2. P. Krantz et al., "A quantum engineer's guide to superconducting qubits," *Appl. Phys. Rev.* 6, 021318 (2019). https://doi.org/10.1063/1.5089550
