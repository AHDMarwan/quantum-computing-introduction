# Shor's Algorithm

## 1. Why Shor's algorithm matters

Shor's algorithm is one of the strongest examples of a quantum algorithm changing the complexity landscape of an important classical problem. It gives polynomial-time quantum algorithms for integer factorization and discrete logarithms, whereas no classical polynomial-time algorithms are known for these problems.

Its importance is both theoretical and practical because widely deployed public-key cryptosystems rely on the difficulty of related number-theoretic problems.

The key conceptual lesson is that Shor's algorithm does **not** factor integers by trying many divisors in parallel. It reduces factoring to a structured periodicity problem and then uses quantum phase/Fourier methods to extract that period efficiently.

## 2. Learning objectives

After this chapter, you should be able to:

- explain the classical reduction from factoring to order finding,
- define the multiplicative order of $a$ modulo $N$,
- derive how an even order yields nontrivial factors,
- explain the role of modular exponentiation,
- connect order finding to quantum phase estimation and the QFT,
- work through a small factoring example,
- distinguish polynomial algorithmic complexity from practical fault-tolerant resource cost,
- and explain the cryptographic consequences without overstating what has been proved about classical hardness.

## 3. The factoring problem

Given a composite integer $N$, the goal is to find nontrivial integers $p$ and $q$ such that

```math
N=pq
```

or, more generally, to recover its prime factorization.

The input size is not $N$ itself but the number of bits needed to represent it:

```math
n=\lceil\log_2 N\rceil.
```

Therefore an algorithm polynomial in $N$ is still exponential in the bit-length $n$. Complexity claims for factoring should be expressed as functions of $\log N$.

## 4. Classical reduction to order finding

Choose a random integer $a$ satisfying

```math
1<a<N.
```

First compute

```math
\gcd(a,N).
```

If this gcd is greater than one, a nontrivial factor has already been found.

Otherwise,

```math
\gcd(a,N)=1.
```

Define the **order** $r$ of $a$ modulo $N$ as the smallest positive integer satisfying

```math
a^r\equiv1\pmod N.
```

Suppose $r$ is even. Then

```math
a^r-1
=
\left(a^{r/2}-1\right)
\left(a^{r/2}+1\right)
```

is divisible by $N$.

If additionally

```math
a^{r/2}\not\equiv-1\pmod N,
```

then the two quantities

```math
\gcd(a^{r/2}-1,N)
```

and

```math
\gcd(a^{r/2}+1,N)
```

produce nontrivial factors with high probability over suitable random choices of $a$.

Thus the hard subproblem becomes:

> Find the order $r$ efficiently.

## 5. Worked example: factoring 15

Take

```math
N=15
```

and choose

```math
a=2.
```

We compute powers modulo 15:

```math
2^1\equiv2\pmod{15},
```

```math
2^2\equiv4\pmod{15},
```

```math
2^3\equiv8\pmod{15},
```

```math
2^4\equiv1\pmod{15}.
```

Therefore

```math
r=4.
```

Since $r$ is even,

```math
a^{r/2}=2^2=4.
```

Also

```math
4\not\equiv-1\pmod{15}.
```

Now compute

```math
\gcd(4-1,15)=3,
```

and

```math
\gcd(4+1,15)=5.
```

Thus

```math
15=3\times5.
```

The quantum computer is needed to obtain the order efficiently for large inputs; the gcd computations and final reconstruction are classical and efficient.

## 6. Periodic structure

Consider the modular-exponentiation function

```math
f(x)=a^x\bmod N.
```

Because $a^r\equiv1\pmod N$,

```math
f(x+r)=f(x).
```

Thus the hidden order $r$ appears as a period.

A quantum computer can represent many $x$ values coherently and use modular arithmetic to create a state whose amplitudes contain this periodic structure.

The useful resource is not merely the superposition; the algorithm needs a Fourier/phase procedure that converts periodicity into measurable information.

## 7. Order finding as phase estimation

A particularly clean formulation uses the unitary multiplication operator

```math
U_a|y\rangle
=
|ay\bmod N\rangle
```

on the appropriate modular subspace.

Repeated application gives

```math
U_a^k|y\rangle
=
|a^k y\bmod N\rangle.
```

Because powers of $a$ cycle with period $r$, the eigenvalues of $U_a$ are related to $r$th roots of unity.

QPE can estimate phases of the form

```math
\frac{s}{r}
```

for integers $s$.

From a sufficiently accurate estimate of such a rational number, classical postprocessing can recover a candidate denominator $r$ using continued fractions.

This is the conceptual bridge:

```text
order finding
-> eigenphase estimation
-> rational reconstruction
-> factors
```

## 8. QFT viewpoint

An equivalent textbook presentation starts with a superposition over exponents and computes modular exponentiation coherently:

```math
\frac1{\sqrt Q}
\sum_{x=0}^{Q-1}
|x\rangle|a^x\bmod N\rangle.
```

The periodic structure in $x$ is then processed by a quantum Fourier transform on the first register.

Measurement produces values concentrated near integer multiples of

```math
\frac{Q}{r}.
```

Classical rational approximation then infers $r$.

The QFT and QPE viewpoints are mathematically closely related; the latter often makes the spectral structure more transparent.

## 9. Why this is not “parallel trial division”

A common but misleading explanation is that the quantum computer tries many possible factors simultaneously.

The actual structure is different:

1. factoring is reduced to order finding;
2. modular arithmetic creates a periodic quantum state;
3. quantum interference extracts frequency/phase information;
4. classical number theory converts the period into factors.

The speedup arises from exploiting algebraic structure, not from reading exponentially many independent candidate answers.

## 10. Complexity perspective

Shor's algorithm runs in time polynomial in

```math
\log N
```

under the standard quantum circuit model.

The exact asymptotic gate complexity depends on the modular-arithmetic implementation and multiplication algorithms used. The dominant high-level cost is typically reversible modular exponentiation rather than the QFT itself.

This distinction matters because the QFT is visually prominent in textbook circuits but is often not the practical bottleneck.

## 11. Resource accounting

A serious implementation analysis must count more than abstract algorithmic steps.

Relevant resources include:

| Resource | Why it matters |
|---|---|
| Logical qubits | Registers and arithmetic workspace |
| Reversible modular multiplication | Dominant arithmetic primitive |
| Non-Clifford gates | Expensive under many fault-tolerant schemes |
| Logical circuit depth | Controls runtime and error budget |
| Error-correction overhead | Converts logical resources to physical resources |
| State preparation and measurement | Smaller but still necessary costs |
| Classical postprocessing | Continued fractions, gcds, verification |

A statement such as “Shor is polynomial-time” is a complexity-theoretic statement, not a claim that current devices can factor cryptographically relevant integers efficiently.

## 12. Failure cases and repetition

A chosen $a$ may fail to produce useful factors if:

- the order $r$ is odd;
- or

```math
a^{r/2}\equiv-1\pmod N.
```

The procedure then chooses another $a$ and repeats.

Also, phase estimation may produce an $s$ that is not coprime with $r$, so the reconstructed denominator may be a divisor of the true order. Candidate orders are therefore verified classically.

The full algorithm is probabilistic but succeeds with high probability after a modest number of repetitions.

## 13. Cryptographic consequence

A sufficiently large fault-tolerant quantum computer running Shor's algorithm would undermine cryptosystems whose security depends on integer factorization or discrete logarithms, including RSA and elliptic-curve cryptography.

This is a major motivation for post-quantum cryptography.

A careful statement is:

> No polynomial-time classical algorithm for general integer factorization is known, while Shor gives a polynomial-time quantum algorithm.

It is **not** known that classical polynomial-time factoring is mathematically impossible.

## 14. Common misconceptions

### “Shor proves factoring is exponentially hard classically.”

No. It proves an efficient quantum algorithm exists. It does not prove a classical lower bound excluding polynomial-time factoring.

### “The QFT alone gives the speedup.”

No. Efficient reversible modular arithmetic, coherent periodic structure, and number-theoretic reduction are all essential.

### “Shor factors numbers by testing all divisors at once.”

No. It solves an order-finding problem.

### “Polynomial time means practical on today's quantum hardware.”

No. Fault-tolerant logical resource requirements are substantial.

## 15. Connections

Shor's algorithm connects several foundational ideas:

- reversible classical computation,
- modular arithmetic,
- phase kickback,
- quantum phase estimation,
- the quantum Fourier transform,
- continued fractions,
- and fault-tolerant resource estimation.

It is therefore a useful case study in how a real quantum advantage emerges from a complete algorithmic stack rather than a single quantum primitive.

## 16. Exercises

### Conceptual

1. Why is complexity measured in $\log N$ rather than $N$?
2. Explain why finding the order of $a$ can reveal factors of $N$.
3. Why is modular exponentiation more central to implementation cost than the visual size of the QFT circuit suggests?
4. Why does Shor not prove a classical lower bound for factoring?

### Computational

5. Factor $N=21$ using $a=2$ by computing the order classically and applying the gcd step.
6. Show algebraically that if $a^r\equiv1\pmod N$ and $r$ is even, then $N$ divides

```math
(a^{r/2}-1)(a^{r/2}+1).
```

7. For a hypothetical order $r=7$, list the ideal QPE eigenphases $s/r$.
8. Explain how continued fractions could recover $r$ from a sufficiently accurate approximation to $s/r$.

### Research-oriented

9. A resource-estimation paper counts logical qubits but omits non-Clifford gate count. What important implementation information is missing?
10. Compare “polynomial-time algorithm” with “cryptographically practical attack” as two different claims.
11. Identify which parts of Shor's algorithm are quantum and which are classical.
12. Explain why improving reversible multiplication can materially change physical resource estimates even though the high-level complexity class remains polynomial.

## 17. Key takeaways

- Shor reduces factoring to order finding.
- Order finding exposes a periodic/spectral structure accessible to QPE or QFT methods.
- Classical continued fractions and gcd computations convert the recovered order into factors.
- The algorithm is polynomial in the bit-length of the input.
- Practical implementation is dominated by fault-tolerant arithmetic and error-correction resources, not merely high-level QFT gates.
- Shor establishes a powerful quantum algorithm but does not prove classical factoring is exponentially hard.

## References

1. P. W. Shor, "Algorithms for quantum computation: discrete logarithms and factoring," *Proceedings of FOCS* (1994). https://doi.org/10.1109/SFCS.1994.365700
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
3. J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
