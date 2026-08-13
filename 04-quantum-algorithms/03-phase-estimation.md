# Quantum Phase Estimation

## 1. Problem

Let $U$ be a unitary and suppose an eigenstate $|u\rangle$ is available such that

```math
U|u\rangle=e^{2\pi i\phi}|u\rangle,
\qquad
\phi\in[0,1).
```

Quantum phase estimation (QPE) estimates $\phi$.

## 2. Phase kickback

An ancilla qubit controlling $U$ transforms

```math
\frac{|0\rangle+|1\rangle}{\sqrt2}|u\rangle
```

into

```math
\frac{|0\rangle+e^{2\pi i\phi}|1\rangle}{\sqrt2}|u\rangle.
```

The eigenvalue phase is transferred to a measurable relative phase on the control register.

## 3. Binary phase encoding

Using $m$ control qubits and controlled powers

```math
U^{2^0},U^{2^1},\ldots,U^{2^{m-1}},
```

the control register accumulates a Fourier-structured phase state. Applying the inverse quantum Fourier transform approximately maps this state to the $m$-bit binary representation of $\phi$.

## 4. Precision and resources

The number of control qubits determines digital precision, while the dominant coherent cost is often implementing large controlled powers of $U$. In Hamiltonian problems where

```math
U=e^{-iHt},
```

phase estimation provides energy estimates because an energy eigenstate obeys

```math
e^{-iHt}|E_j\rangle=e^{-iE_jt}|E_j\rangle.
```

## 5. Importance

QPE is a primitive inside major fault-tolerant quantum algorithms, including Shor-type order finding and high-precision quantum chemistry methods. It also exposes an important distinction from VQE: QPE can provide eigenvalues through coherent phase extraction, whereas VQE estimates energies variationally using repeated expectation measurements and classical optimization.

## 6. Assumptions

The textbook algorithm assumes

- access to an eigenstate with sufficient overlap,
- controlled implementations of powers of $U$,
- long enough coherent evolution,
- and fault rates compatible with the required circuit depth.

These assumptions strongly influence practical resource estimates.

## References

1. A. Y. Kitaev, "Quantum measurements and the Abelian Stabilizer Problem" (1995). https://arxiv.org/abs/quant-ph/9511026
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
