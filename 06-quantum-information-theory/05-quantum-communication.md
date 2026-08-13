# Quantum Communication

## 1. Sending quantum and classical information

Quantum communication studies how information can be transmitted when channels and information carriers are quantum. Tasks include

- transmitting unknown quantum states,
- sending classical information through quantum channels,
- distributing entanglement,
- quantum key distribution,
- teleportation,
- and networked quantum computation.

## 2. Teleportation

Suppose Alice and Bob share a Bell pair. Alice also holds an unknown qubit \(|\psi\rangle\). Quantum teleportation allows Bob to recover \(|\psi\rangle\) using

- one shared ebit,
- a Bell-basis measurement by Alice,
- and two classical bits sent to Bob.

No faster-than-light communication occurs because Bob cannot reconstruct the state until the classical message arrives.

Teleportation also does not violate no-cloning: Alice's original state is destroyed by the protocol.

## 3. Superdense coding

With a shared Bell pair, Alice can encode two classical bits by applying one of four local Pauli operations and sending one qubit to Bob. Bob performs a Bell measurement and recovers two bits.

Teleportation and superdense coding illustrate tradeoffs among qubits, classical bits, and shared entanglement.

## 4. Quantum channel capacity

Different capacities answer different questions. Examples include

- classical capacity,
- quantum capacity,
- private classical capacity,
- and entanglement-assisted capacity.

There is no single universal “capacity of a quantum channel.” The operational task and allowed assistance must be specified.

## 5. No-cloning and repeaters

Classical repeaters can copy and amplify signals. Unknown quantum states cannot be cloned, so long-distance quantum networking requires different strategies, such as entanglement swapping, purification/error correction, and quantum repeaters.

## 6. Relation to distributed computation and QML

Quantum networks may support distributed sensing, blind computation, delegated learning, and models where quantum data remain distributed across nodes. Communication complexity can then become the relevant resource rather than local gate count.

## References

1. C. H. Bennett et al., "Teleporting an unknown quantum state via dual classical and EPR channels," *Phys. Rev. Lett.* 70, 1895 (1993). https://doi.org/10.1103/PhysRevLett.70.1895
2. C. H. Bennett and S. J. Wiesner, "Communication via one- and two-particle operators on Einstein-Podolsky-Rosen states," *Phys. Rev. Lett.* 69, 2881 (1992). https://doi.org/10.1103/PhysRevLett.69.2881
3. M. M. Wilde, *Quantum Information Theory*, Cambridge University Press.
