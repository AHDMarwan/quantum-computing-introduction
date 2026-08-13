# Shor's Algorithm

## 1. Why Shor's algorithm matters

Shor's algorithm gives polynomial-time quantum algorithms for integer factorization and discrete logarithms. Its importance comes from both complexity theory and cryptography: widely deployed public-key schemes rely on the apparent classical hardness of related number-theoretic problems.

## 2. Factoring reduces to order finding

To factor an odd composite integer $N$, choose $a<N$ with

```math
\gcd(a,N)=1.
```

The order $r$ of $a$ modulo $N$ is the smallest positive integer such that

```math
a^r\equiv1\pmod N.
```

If $r$ is even and

```math
a^{r/2}\not\equiv-1\pmod N,
```

then nontrivial factors can be obtained from

```math
\gcd(a^{r/2}\pm1,N).
```

The quantum part solves order finding efficiently.

## 3. Periodicity and Fourier analysis

Modular exponentiation creates a periodic structure related to

```math
f(x)=a^x\bmod N.
```

A quantum Fourier transform or an equivalent phase-estimation formulation extracts information about the period $r$. Classical continued-fraction processing then reconstructs a candidate order.

## 4. Complexity perspective

The dramatic result is not that a quantum computer tries divisors in superposition. The essential structure is the reduction to a hidden periodicity problem and efficient quantum Fourier/phase processing.

The end-to-end resource cost includes reversible modular arithmetic, error correction, logical qubits, non-Clifford gates, and coherent depth. Practical fault-tolerant resource estimates are therefore much more informative than simply counting the high-level QFT gates.

## 5. Cryptographic consequence

A sufficiently large fault-tolerant quantum computer running Shor's algorithm would break RSA and elliptic-curve cryptography at relevant key sizes. This motivates post-quantum cryptography, whose security is based on different problem families intended to resist known quantum attacks.

## References

1. P. W. Shor, "Algorithms for quantum computation: discrete logarithms and factoring," FOCS 1994. https://doi.org/10.1109/SFCS.1994.365700
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
