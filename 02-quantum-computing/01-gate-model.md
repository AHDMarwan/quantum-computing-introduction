# Gate-Based / Circuit Quantum Computing

## 1. Circuit abstraction

The quantum circuit model represents computation through registers, gates, and measurements. An ideal closed-system circuit acts as

\[
|\psi_{\rm out}\rangle
=
U_LU_{L-1}\cdots U_1|\psi_{\rm in}\rangle.
\]

The ordering matters because quantum gates need not commute.

## 2. Elementary gates and universality

Single-qubit gates together with a suitable entangling two-qubit gate form universal sets. A common theoretical set is

\[
\{H,T,\operatorname{CNOT}\}.
\]

Universality means arbitrary unitary transformations can be approximated to prescribed accuracy using sequences from the gate set.

In fault-tolerant computing, the choice of logical gate set and the cost of non-Clifford resources are especially important.

## 3. Reversibility and measurement

Unitary gates are reversible:

\[
U^{-1}=U^\dagger.
\]

Measurement is not modeled as an ordinary reversible gate because it creates classical outcomes and, depending on the instrument, changes the state conditionally.

A typical algorithm therefore has the form

```text
prepare → coherent gates → interference → measurement → classical output
```

## 4. Circuit complexity

Important resources include

- number of qubits,
- gate count,
- circuit depth,
- two-qubit-gate count,
- connectivity/routing overhead,
- measurements or shots,
- ancilla qubits,
- and, in fault-tolerant settings, logical non-Clifford cost.

Two circuits implementing the same unitary may have very different practical costs.

## 5. Oracles

Many quantum algorithms are analyzed in an oracle or query model. An oracle can encode a function coherently, for example

\[
U_f|x,y\rangle=|x,y\oplus f(x)\rangle.
\]

A query-complexity advantage does not automatically imply an end-to-end runtime advantage unless the oracle access is physically justified and its implementation cost is included.

## 6. Circuit model and QML

Most parameterized quantum circuits used in QML are gate-model objects of the form

\[
U(\boldsymbol\theta,x).
\]

They combine data-dependent gates, trainable gates, entangling operations, and measurement. The circuit is the model implementation; the surrounding loss, optimizer, and data-access assumptions define the learning algorithm.

## References

1. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
2. A. Y. Kitaev, A. Shen, and M. Vyalyi, *Classical and Quantum Computation*, AMS, 2002.
3. J. Preskill, *Quantum Computation Lecture Notes*: https://www.preskill.caltech.edu/ph229/
