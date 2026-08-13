# Quantum Phase Estimation

## 1. Why phase estimation matters

Quantum phase estimation (QPE) is one of the central primitives of fault-tolerant quantum algorithms. It converts an eigenvalue phase of a unitary transformation into an approximately classical binary number.

The algorithm sits behind order finding, many eigenvalue algorithms, high-precision quantum chemistry proposals, and several quantum algorithms built around spectral information.

## 2. Learning objectives

After this chapter, you should be able to:

- state the phase-estimation problem precisely,
- derive phase kickback for an eigenstate,
- explain why controlled powers of $U$ encode binary phase information,
- derive the Fourier-structured control-register state,
- explain the role of the inverse quantum Fourier transform,
- relate phase precision to coherent evolution time and controlled-unitary cost,
- analyze what happens when the input is not an exact eigenstate,
- and distinguish QPE resource requirements from those of variational eigensolvers.

## 3. Problem statement

Let $U$ be a unitary operator and suppose

```math
U|u\rangle
=
e^{2\pi i\phi}|u\rangle,
```

where

```math
\phi\in[0,1).
```

The goal is to estimate the eigenphase $\phi$.

The phase is defined modulo one because

```math
e^{2\pi i(\phi+k)}=e^{2\pi i\phi}
```

for any integer $k$.

## 4. Single-qubit phase kickback

Start a control qubit in

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}
```

and the target register in $|u\rangle$.

A controlled-$U$ operation gives

```math
\frac1{\sqrt2}
\left(
|0\rangle|u\rangle
+
|1\rangle U|u\rangle
\right).
```

Using the eigenvalue equation,

```math
\frac1{\sqrt2}
\left(
|0\rangle
+
e^{2\pi i\phi}|1\rangle
\right)|u\rangle.
```

The target register remains in the same eigenstate while the eigenvalue appears as a relative phase on the control qubit.

This is **phase kickback**.

## 5. Encoding many phase bits

Use $m$ control qubits initialized in

```math
|0\rangle^{\otimes m}.
```

After Hadamards,

```math
\frac{1}{\sqrt{2^m}}
\sum_{k=0}^{2^m-1}|k\rangle.
```

The controlled operations collectively implement

```math
|k\rangle|u\rangle
\longmapsto
|k\rangle U^k|u\rangle.
```

Because

```math
U^k|u\rangle
=
e^{2\pi i k\phi}|u\rangle,
```

the joint state becomes

```math
\frac{1}{\sqrt{2^m}}
\sum_{k=0}^{2^m-1}
e^{2\pi i k\phi}|k\rangle|u\rangle.
```

The phase information is now encoded in a discrete Fourier pattern over the control register.

## 6. Why controlled powers appear

Writing the binary integer $k$ as

```math
k
=
\sum_{j=0}^{m-1}k_j2^j,
```

we have

```math
U^k
=
\prod_{j=0}^{m-1}
\left(U^{2^j}\right)^{k_j}.
```

Therefore one can generate the phase state using controlled powers

```math
U,
U^2,
U^4,
\ldots,
U^{2^{m-1}}.
```

This decomposition explains both the elegant binary structure of QPE and one of its largest resource costs: high precision requires access to long coherent powers of $U$.

## 7. Inverse quantum Fourier transform

If the phase has an exact $m$-bit expansion

```math
\phi
=
\frac{j}{2^m}
```

for some integer $j$, then the control-register state is

```math
\frac{1}{\sqrt{2^m}}
\sum_{k=0}^{2^m-1}
e^{2\pi i jk/2^m}|k\rangle.
```

This is precisely the quantum Fourier transform of $|j\rangle$:

```math
\mathrm{QFT}|j\rangle
=
\frac{1}{\sqrt{2^m}}
\sum_k e^{2\pi i jk/2^m}|k\rangle.
```

Therefore

```math
\mathrm{QFT}^{\dagger}
```

maps the control register to

```math
|j\rangle.
```

Measuring the register returns the binary representation of $\phi$ exactly in this special case.

## 8. Nonexact phases

If $\phi$ is not exactly representable with $m$ bits, the inverse QFT produces a probability distribution concentrated near integers $j$ satisfying

```math
\frac{j}{2^m}\approx\phi.
```

Increasing $m$ narrows the phase resolution.

At the high level,

```math
\text{phase resolution}
\sim
2^{-m}.
```

But this does **not** mean exponentially precise phase information is obtained at only linear physical cost, because implementing the largest controlled power requires evolution proportional to approximately

```math
2^{m-1}.
```

Precision must therefore be analyzed against total coherent evolution time, not just the number of ancilla qubits.

## 9. Worked example: exactly representable phase

Suppose

```math
U|u\rangle
=
e^{2\pi i(3/8)}|u\rangle.
```

Using $m=3$ control qubits, the phase has the exact binary form

```math
\phi
=
\frac38
=0.011_2.
```

After phase kickback, the control register is

```math
\frac1{\sqrt8}
\sum_{k=0}^{7}
e^{2\pi i(3k/8)}|k\rangle.
```

Applying the inverse QFT yields

```math
|011\rangle.
```

Measurement returns the integer $3$, corresponding to

```math
\phi=3/8.
```

## 10. QPE for Hamiltonian eigenvalues

Suppose

```math
H|E_j\rangle
=
E_j|E_j\rangle.
```

Choose a unitary evolution

```math
U=e^{-iHt}.
```

Then

```math
U|E_j\rangle
=
e^{-iE_jt}|E_j\rangle.
```

Thus QPE estimates the phase associated with the energy.

Care is needed with scaling and phase wrapping: the relationship between energy and phase must be chosen so that the energy interval of interest maps unambiguously into the unit circle.

## 11. What if the input is not an eigenstate?

Suppose

```math
|\psi\rangle
=
\sum_j c_j|u_j\rangle,
```

where

```math
U|u_j\rangle
=
e^{2\pi i\phi_j}|u_j\rangle.
```

Linearity gives a superposition of phase-estimation branches. Measurement returns an estimate of $\phi_j$ with probability approximately

```math
|c_j|^2.
```

The target register is correspondingly projected toward the associated eigenspace.

Therefore state preparation matters: if the desired eigenstate has tiny overlap with the prepared state, many repetitions may be required.

## 12. Resource accounting

A useful QPE resource table is:

| Resource | Role |
|---|---|
| Control qubits | Digital phase precision |
| Controlled $U^{2^j}$ | Coherent phase accumulation |
| Maximum evolution time | Sets achievable spectral resolution |
| Inverse QFT | Converts phase pattern into binary information |
| Initial-state overlap | Controls probability of obtaining desired eigenvalue |
| Fault tolerance | Needed for sufficiently deep coherent execution |

A naive QFT on $m$ qubits uses $O(m^2)$ elementary controlled rotations, although approximate implementations can reduce this overhead. In many applications, however, controlled time evolution or controlled arithmetic dominates the cost.

## 13. QPE versus VQE

Both can be used to estimate eigenvalues, but the computational paradigms are different.

### QPE

```text
prepare state
-> long coherent controlled evolution
-> inverse QFT / phase extraction
-> eigenvalue estimate
```

### VQE

```text
parameterized state
-> repeated expectation measurements
-> classical optimization
-> energy estimate
```

QPE can achieve systematic high precision in a fault-tolerant setting but requires long coherent circuits and suitable state overlap. VQE trades this coherent depth for repeated measurements and a difficult classical-quantum optimization problem.

Neither method is universally preferable independent of the hardware regime and task.

## 14. Common misconceptions

### “Each extra QPE qubit gives a free extra bit of precision.”

No. It also demands access to larger powers of $U$ or longer coherent evolution.

### “QPE can find any eigenvalue without preparing an eigenstate.”

A general input yields eigenvalues according to its spectral overlaps. Small desired overlap can be a major cost.

### “The QFT is always the dominant cost.”

Often it is not. Controlled simulation, arithmetic, or oracle implementation can dominate.

### “QPE directly measures energy.”

QPE measures a phase of a chosen unitary. Energy estimation follows after mapping a Hamiltonian eigenvalue into that phase.

## 15. Connections

QPE is tightly connected to:

- Shor's order-finding algorithm,
- Hamiltonian simulation,
- quantum chemistry,
- amplitude estimation,
- spectral algorithms,
- and fault-tolerant resource estimation.

Conceptually, it is the mature version of phase kickback first seen in simpler oracle algorithms.

## 16. Exercises

### Conceptual

1. Why must the target register be in an eigenstate for clean phase kickback?
2. Why does increasing the number of control qubits increase coherent-time requirements?
3. Explain why QPE estimates a unitary phase rather than an eigenvalue of an arbitrary Hermitian operator directly.
4. Why can state-preparation overlap dominate the repetition cost?

### Computational

5. Show that controlled powers $U^{2^j}$ reproduce controlled $U^k$ when $k$ is encoded in binary.
6. For $\phi=5/8$, write the three-qubit phase state and state the ideal QPE output.
7. If $U=e^{-iHt}$ and $H|E\rangle=E|E\rangle$, derive the relation between $E$ and the measured phase.
8. Suppose $|\psi\rangle=\sqrt{0.9}|u_0\rangle+\sqrt{0.1}|u_1\rangle$. What phase outcomes should QPE produce in the ideal limit?

### Research-oriented

9. A paper reports $m$ bits of QPE precision but counts only $m$ ancilla qubits. What missing resource should you immediately ask for?
10. Compare a QPE-based and a VQE-based ground-state algorithm using coherent depth, state preparation, measurement count, and optimization assumptions.
11. Under what conditions could approximate or iterative phase-estimation variants be preferable to textbook QPE?

## 17. Key takeaways

- QPE converts an eigenvalue phase of a unitary into an approximate binary number.
- Controlled powers encode phase information through phase kickback.
- The inverse QFT decodes the resulting Fourier structure.
- Precision is tied to coherent evolution time, not just ancilla count.
- State overlap controls which eigenphase is observed.
- QPE is a foundational primitive for Shor's algorithm and fault-tolerant spectral computation.

## References

1. A. Y. Kitaev, "Quantum measurements and the Abelian Stabilizer Problem." https://arxiv.org/abs/quant-ph/9511026
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
3. J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
