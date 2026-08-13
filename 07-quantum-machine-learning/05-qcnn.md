# Quantum Convolutional and Structured Architectures

## 1. Why structure matters

A generic hardware-efficient PQC ignores many properties of the learning problem. Structured quantum architectures instead encode locality, symmetry, graph structure, scale, or recurrence directly into the circuit or channel.

The quantum convolutional neural network (QCNN) is a canonical example.

## 2. QCNN architecture

A QCNN alternates local unitary “convolution” layers with pooling/coarse-graining operations. Conceptually,

```text
local quantum features
      ↓
convolution
      ↓
pooling / coarse graining
      ↓
convolution
      ↓
...
      ↓
small readout subsystem
```

The architecture resembles multiscale renormalization ideas more closely than a literal classical CNN with copied filters and nonlinear activations.

## 3. Motivation

For data with local structure, the number of trainable parameters can scale more favorably than a dense generic circuit. QCNNs have been proposed for tasks such as quantum phase recognition and error-correction-inspired classification.

## 4. Structured QNN families

Other examples include

- quantum graph neural networks,
- tensor-network-inspired circuits,
- equivariant quantum models,
- recurrent quantum models,
- dissipative quantum neural networks,
- and problem-specific message-passing architectures.

The phrase “QNN” should therefore be accompanied by an architectural definition.

## 5. Inductive bias

The central ML idea is inductive bias. A model should not represent every function equally well; it should privilege structures expected in the task.

For quantum data, useful biases may come from

- locality,
- translational invariance,
- particle-number conservation,
- gauge symmetries,
- permutation symmetry,
- causal structure,
- or entanglement scale.

## 6. Architecture versus quantum advantage

A structured quantum model can outperform an unstructured PQC without demonstrating quantum advantage. The correct comparison should include structured classical methods and, when possible, classical tensor-network or kernel baselines matched to the same physical prior.

## References

1. I. Cong, S. Choi, and M. D. Lukin, "Quantum convolutional neural networks," *Nat. Phys.* 15, 1273–1278 (2019). https://doi.org/10.1038/s41567-019-0648-8
