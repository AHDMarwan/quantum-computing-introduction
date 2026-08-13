# Quantum Entropy and Information

## 1. Why entropy matters in quantum information

Entropy quantifies uncertainty, mixedness, correlation, compressibility, and communication limits. In quantum information theory, it also reveals phenomena with no direct classical analogue, such as negative conditional entropy for entangled states.

The central object is the von Neumann entropy

```math
S(\rho)
=
-\mathrm{Tr}(\rho\log\rho).
```

When logarithms are base 2, entropy is measured in bits.

## 2. Learning objectives

After this chapter, you should be able to:

- compute von Neumann entropy from eigenvalues,
- distinguish entropy of a pure state from entropy of a subsystem,
- define joint, conditional, and mutual information,
- explain why quantum conditional entropy can be negative,
- define quantum relative entropy and its data-processing inequality,
- define the Holevo quantity and interpret accessible classical information,
- connect entropy to distinguishability and correlations,
- and identify how information measures appear in QML and quantum learning theory.

## 3. Von Neumann entropy

Let

```math
\rho
=
\sum_i\lambda_i|i\rangle\langle i|
```

be the spectral decomposition of a density operator.

Then

```math
S(\rho)
=
-\sum_i\lambda_i\log\lambda_i.
```

Thus von Neumann entropy is simply the Shannon entropy of the eigenvalue distribution.

## 4. Pure states

For a pure state,

```math
\rho
=
|\psi\rangle\langle\psi|,
```

its eigenvalues are

```math
1,0,0,\ldots.
```

Therefore

```math
S(\rho)=0.
```

A pure state can contain nontrivial superposition and entanglement while having zero entropy as a complete closed system.

## 5. Maximally mixed state

For a $d$-dimensional maximally mixed state,

```math
\rho_*
=
\frac{I}{d},
```

the eigenvalues are all $1/d$.

Therefore

```math
S(\rho_*)
=
-\sum_{i=1}^{d}
\frac1d\log\frac1d
=
\log d.
```

This is the maximum possible entropy on a $d$-dimensional Hilbert space.

## 6. Entropy and basis independence

Although a density matrix changes representation under a basis transformation,

```math
\rho
\mapsto
U\rho U^\dagger,
```

its eigenvalues do not change.

Therefore

```math
S(U\rho U^\dagger)
=
S(\rho).
```

Von Neumann entropy is a property of the state, not of a chosen coordinate basis.

## 7. Worked example: qubit mixture

Consider

```math
\rho
=
p|0\rangle\langle0|
+(1-p)|1\rangle\langle1|.
```

Its entropy is

```math
S(\rho)
=
-p\log p
-(1-p)\log(1-p).
```

For

```math
p=\frac12,
```

we obtain

```math
S(\rho)=1
```

bit.

For $p=0$ or $p=1$,

```math
S(\rho)=0.
```

## 8. Joint systems

For a bipartite state $\rho_{AB}$, define

```math
S(A)=S(\rho_A),
```

```math
S(B)=S(\rho_B),
```

```math
S(AB)=S(\rho_{AB}).
```

The reduced states are

```math
\rho_A=\mathrm{Tr}_B(\rho_{AB}),
```

```math
\rho_B=\mathrm{Tr}_A(\rho_{AB}).
```

The relation between local and joint entropy encodes correlation structure.

## 9. Product states

If

```math
\rho_{AB}
=
\rho_A\otimes\rho_B,
```

then entropy is additive:

```math
S(AB)
=
S(A)+S(B).
```

This is the entropy analogue of statistical independence.

## 10. Pure entangled states

For a bipartite pure state

```math
|\psi\rangle_{AB},
```

the global entropy is

```math
S(AB)=0.
```

But if the state is entangled, the reduced states are mixed and satisfy

```math
S(A)=S(B)>0.
```

For a Bell state,

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2},
```

we have

```math
S(AB)=0,
```

and

```math
S(A)=S(B)=1.
```

The local uncertainty comes entirely from entanglement with the other subsystem.

## 11. Quantum conditional entropy

Define

```math
S(A|B)
=
S(AB)-S(B).
```

Classically, conditional Shannon entropy is nonnegative.

Quantum mechanically, it can be negative.

For a Bell pair,

```math
S(A|B)
=
0-1
=-1.
```

This negative value is not a probability paradox. It reflects genuinely quantum correlation and has operational meaning in tasks such as state merging.

## 12. Mutual information

Quantum mutual information is

```math
I(A:B)
=
S(A)+S(B)-S(AB).
```

It measures total correlation between $A$ and $B$.

For a product state,

```math
I(A:B)=0.
```

For a Bell pair,

```math
I(A:B)=2.
```

bits when logarithms are base 2.

The value can exceed the entropy of either subsystem because quantum mutual information counts total correlation structure.

## 13. Relative entropy

Quantum relative entropy is

```math
D(\rho\|\sigma)
=
\mathrm{Tr}
\left[
\rho(
\log\rho-
\log\sigma)
\right],
```

when the support condition is satisfied.

It is not symmetric:

```math
D(\rho\|\sigma)
\neq
D(\sigma\|\rho)
```

in general.

Therefore it is not a metric distance.

## 14. Positivity of relative entropy

Quantum relative entropy satisfies

```math
D(\rho\|\sigma)
\ge0,
```

with equality exactly when

```math
\rho=\sigma
```

under the usual finite-dimensional conditions.

This makes it a useful measure of statistical distinguishability.

## 15. Mutual information as relative entropy

A central identity is

```math
I(A:B)
=
D
\left(
\rho_{AB}
\middle\|
\rho_A\otimes\rho_B
\right).
```

Thus mutual information measures how distinguishable the joint state is from the product of its marginals.

Correlation means precisely that

```math
\rho_{AB}
\neq
\rho_A\otimes\rho_B.
```

## 16. Data-processing inequality

For every quantum channel $\mathcal E$,

```math
D(\rho\|\sigma)
\ge
D
\left(
\mathcal E(\rho)
\middle\|
\mathcal E(\sigma)
\right).
```

Physical processing cannot make two states more distinguishable according to relative entropy.

This is a quantum version of a broad information-theoretic principle:

> Processing cannot create information about which input was present if that information was not already available.

## 17. Mutual-information data processing

If local channels act on a bipartite system,

```math
\rho_{AB}
\mapsto
(\mathcal E_A\otimes\mathcal F_B)(\rho_{AB}),
```

then total mutual information cannot increase under independent local processing.

This formalizes the intuition that local noise cannot create correlations from nowhere.

## 18. Classical-quantum ensembles

Suppose a classical random variable $X$ takes value $x$ with probability $p_x$ and is encoded in a quantum state $\rho_x$.

The joint classical-quantum state is

```math
\rho_{XQ}
=
\sum_x
p_x
|x\rangle\langle x|
\otimes
\rho_x.
```

Its average quantum state is

```math
\bar\rho
=
\sum_xp_x\rho_x.
```

This formalism is fundamental for communication and learning from quantum states.

## 19. Holevo information

The Holevo quantity of the ensemble is

```math
\chi
=
S(\bar\rho)
-
\sum_xp_xS(\rho_x).
```

It bounds the amount of classical information that can be extracted from the ensemble by measurement.

This is one of the clearest reasons why an exponentially large Hilbert space does not imply exponentially many readable classical bits from one state preparation.

## 20. Pure-state ensemble example

If every $\rho_x$ is pure, then

```math
S(\rho_x)=0.
```

Therefore

```math
\chi
=
S(\bar\rho).
```

Even though individual states may be vectors in a high-dimensional complex space, accessible classical information remains constrained by the ensemble geometry and measurement process.

## 21. Entropy versus accessible information

Entropy of a quantum state is not automatically “the number of classical bits stored inside it.”

Different quantities answer different operational questions:

- $S(\rho)$: mixedness/compressibility,
- $I(A:B)$: total correlation,
- $D(\rho\|\sigma)$: distinguishability,
- $\chi$: upper bound on accessible classical information from an ensemble.

Using the word “information” without specifying which quantity is often too vague for rigorous quantum-information analysis.

## 22. Entropy and measurement

Measurement converts quantum states into classical distributions.

For POVM $\{E_y\}$,

```math
p(y)
=
\mathrm{Tr}(E_y\rho).
```

The Shannon entropy

```math
H(Y)
```

of the outcome distribution depends on the measurement.

By contrast,

```math
S(\rho)
```

is basis independent.

Therefore measurement entropy and state entropy are different objects.

## 23. Entropy and entanglement

For bipartite pure states, local entropy is an entanglement measure:

```math
E(|\psi\rangle)
=
S(\rho_A)
=
S(\rho_B).
```

For mixed states, however, local entropy includes both classical and quantum uncertainty and is not by itself an entanglement measure.

This distinction motivates the more sophisticated mixed-state measures in the next chapter.

## 24. Entropy in quantum learning

Information quantities appear naturally in QML.

Examples include:

- information bottlenecks,
- quantum representation compression,
- mutual-information feature selection,
- generalization analyses,
- state discrimination,
- channel discrimination,
- quantum sufficient statistics.

A learning objective need not always be a scalar prediction loss. It can be an operational information quantity.

## 25. Quantum information bottleneck viewpoint

Suppose a model maps an input $X$ into a quantum representation $Q$ relevant to target $Y$.

One can imagine optimizing a tradeoff such as

```math
\mathcal L
=
I(X:Q)
-
\beta I(Q:Y).
```

The first term penalizes retained input information; the second rewards predictive information.

This creates a quantum analogue of information-bottleneck reasoning and connects directly to the idea of learning compressed quantum representations rather than maximizing Hilbert-space dimension.

## 26. Common misconceptions

### “Pure state means zero uncertainty in every measurement.”

No. Pure state means zero von Neumann entropy. Measurement outcomes in a non-eigenbasis can still be random.

### “The entropy of a subsystem of a pure state must be zero.”

No. Entanglement can make the reduced state mixed.

### “Negative conditional entropy means negative probability.”

No. It is an information-theoretic quantity with no classical analogue, not a probability.

### “A $2^n$-dimensional state can reveal $2^n$ classical amplitudes in one measurement.”

No. Accessible information is constrained by quantum measurement and results such as the Holevo bound.

### “Relative entropy is a distance metric.”

No. It is generally asymmetric and does not satisfy metric axioms.

## 27. Exercises

### Conceptual

1. Why can a pure bipartite state have mixed reduced states?
2. Explain why von Neumann entropy is basis independent.
3. What operational distinction separates mutual information from entanglement?
4. Why does the Holevo quantity matter when discussing quantum feature spaces?

### Computational

5. Compute $S(\rho)$ for

```math
\rho
=
\begin{pmatrix}
3/4&0\\
0&1/4
\end{pmatrix}.
```
6. Compute $S(A)$, $S(B)$, $S(AB)$, $S(A|B)$, and $I(A:B)$ for a Bell pair.
7. Show that a product state has zero mutual information.
8. For two equiprobable orthogonal pure states, compute the Holevo quantity.

### Research-oriented

9. A QML paper argues that an $n$-qubit embedding stores exponentially many classical features. Which information-theoretic questions should be asked before accepting that interpretation?
10. Design a learning objective based on mutual information rather than classification error.
11. How could data processing provide a no-go argument for recovering information lost during a noisy encoding stage?
12. Formulate a quantum-information-bottleneck problem for learning from quantum states.

## 28. Key takeaways

- Von Neumann entropy measures mixedness and equals the entropy of the state's eigenvalues.
- Pure global states can have mixed local states because of entanglement.
- Quantum conditional entropy can be negative.
- Mutual information measures total correlation and can be expressed as relative entropy.
- Relative entropy decreases under quantum channels through data processing.
- The Holevo quantity limits accessible classical information from quantum ensembles.
- Quantum information measures provide rigorous tools for analyzing representation, compression, distinguishability, and learning.

## References

1. J. von Neumann, *Mathematical Foundations of Quantum Mechanics*.
2. A. S. Holevo, "Bounds for the quantity of information transmitted by a quantum communication channel," *Problems of Information Transmission* 9 (1973).
3. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
4. M. M. Wilde, *Quantum Information Theory*, Cambridge University Press.
