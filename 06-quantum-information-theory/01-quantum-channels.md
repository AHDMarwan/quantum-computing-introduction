# Quantum Channels

## 1. Why channels are the natural language of physical quantum processes

Unitary evolution is only the closed-system limit of quantum dynamics. Real quantum systems interact with environments, lose information, undergo measurements, are reset, and experience noise.

The general deterministic transformation of a quantum state is a **completely positive trace-preserving** (CPTP) linear map

```math
\mathcal E:
\mathcal L(\mathcal H_A)
\rightarrow
\mathcal L(\mathcal H_B).
```

A channel maps every valid input density operator to a valid output density operator.

## 2. Learning objectives

After this chapter, you should be able to:

- define positivity, complete positivity, and trace preservation,
- explain why complete positivity is required for systems entangled with references,
- derive and use Kraus representations,
- verify trace-preservation conditions,
- construct basic noise channels,
- explain Stinespring dilation,
- define the Choi representation,
- connect channels to measurements and instruments,
- and interpret trainable open-system QML models as parameterized channels rather than only unitaries.

## 3. Positivity

A density operator satisfies

```math
\rho\succeq0,
\qquad
\mathrm{Tr}(\rho)=1.
```

A physical transformation must therefore satisfy

```math
\rho\succeq0
\Longrightarrow
\mathcal E(\rho)\succeq0.
```

This property is called positivity.

But positivity alone is not sufficient.

## 4. Why complete positivity?

Suppose system $A$ is entangled with an untouched reference $R$.

A local operation on $A$ acts as

```math
\mathcal E_A\otimes I_R.
```

Even if $\mathcal E_A$ maps every isolated state of $A$ to a positive operator, the joint map could fail to preserve positivity on entangled states unless $\mathcal E_A$ is **completely positive**.

Complete positivity requires that for every reference dimension $k$,

```math
\mathcal E\otimes I_k
```

is positive.

This is an operational requirement, not merely a technical mathematical preference: a local physical process must remain valid even when its input is part of a larger entangled system.

## 5. Trace preservation

A deterministic process must preserve total probability:

```math
\mathrm{Tr}[\mathcal E(\rho)]
=
\mathrm{Tr}(\rho)
=1.
```

Thus a deterministic quantum channel is CPTP.

Non-trace-preserving completely positive maps also appear. They describe individual outcomes of measurements or probabilistic branches. A collection of such maps can sum to a trace-preserving instrument.

## 6. Kraus representation

Every finite-dimensional quantum channel admits an operator-sum representation

```math
\mathcal E(\rho)
=
\sum_k
K_k\rho K_k^\dagger.
```

The operators $K_k$ are Kraus operators.

Trace preservation requires

```math
\sum_kK_k^\dagger K_k
=I.
```

### Derivation of the trace-preserving condition

Using cyclicity of trace,

```math
\mathrm{Tr}[\mathcal E(\rho)]
=
\sum_k
\mathrm{Tr}(K_k\rho K_k^\dagger)
```

```math
=
\sum_k
\mathrm{Tr}(K_k^\dagger K_k\rho)
```

```math
=
\mathrm{Tr}
\left[
\left(
\sum_kK_k^\dagger K_k
\right)\rho
\right].
```

For this to equal $\mathrm{Tr}(\rho)$ for every $\rho$, we require

```math
\sum_kK_k^\dagger K_k=I.
```

## 7. Kraus representations are not unique

The same physical channel can have many Kraus decompositions.

If $\{K_j\}$ is a Kraus set and $u_{aj}$ is an appropriate isometry, then

```math
L_a
=
\sum_j u_{aj}K_j
```

can describe the same channel.

Therefore individual Kraus operators should not generally be interpreted as uniquely defined physical events unless a specific environment measurement or instrument fixes such an interpretation.

The channel $\mathcal E$ is the invariant physical object.

## 8. Example: unitary channel

A unitary transformation is the special case with one Kraus operator:

```math
K_1=U.
```

Then

```math
\mathcal E_U(\rho)
=
U\rho U^\dagger.
```

Since

```math
U^\dagger U=I,
```

the trace-preserving condition is satisfied.

Thus unitary evolution is a strict subset of quantum channels.

## 9. Example: dephasing channel

A simple qubit dephasing channel can be written

```math
\mathcal E_p(\rho)
=
(1-p)\rho
+pZ\rho Z.
```

One Kraus representation is

```math
K_0=\sqrt{1-p}\,I,
```

```math
K_1=\sqrt p\,Z.
```

The trace-preservation condition is

```math
K_0^\dagger K_0
+K_1^\dagger K_1
=
(1-p)I+pI=I.
```

In the computational basis, dephasing suppresses off-diagonal coherence while preserving populations.

## 10. Example: amplitude damping

Amplitude damping models energy relaxation, for example

```math
|1\rangle
\rightarrow
|0\rangle.
```

A standard Kraus representation is

```math
K_0
=
\begin{pmatrix}
1&0\\
0&\sqrt{1-\gamma}
\end{pmatrix},
```

```math
K_1
=
\begin{pmatrix}
0&\sqrt\gamma\\
0&0
\end{pmatrix}.
```

The excited-state population decays with probability $\gamma$.

Unlike dephasing, amplitude damping is nonunital:

```math
\mathcal E(I)
\neq
I.
```

This reflects directional relaxation toward the ground state.

## 11. Unital versus nonunital channels

A channel is unital if

```math
\mathcal E(I)=I.
```

Depolarizing and dephasing channels are common unital examples. Amplitude damping is not.

Unitality matters because it captures whether the maximally mixed state is preserved.

It also affects entropy and resource behavior.

## 12. Stinespring dilation

Every quantum channel can be represented as unitary evolution on a larger system followed by discarding an environment:

```math
\mathcal E(\rho)
=
\mathrm{Tr}_E
\left[
U
(\rho\otimes|0\rangle\langle0|_E)
U^\dagger
\right].
```

This is the Stinespring dilation picture.

It explains how apparently irreversible dynamics emerge from reversible dynamics on a larger Hilbert space:

```text
system information
-> system-environment correlations
-> environment discarded
-> apparent irreversibility.
```

## 13. Kraus operators from a dilation

Choose an orthonormal environment basis $\{|k\rangle_E\}$ and define

```math
K_k
=
{}_E\langle k|
U
|0\rangle_E.
```

Then tracing out the environment gives

```math
\mathcal E(\rho)
=
\sum_kK_k\rho K_k^\dagger.
```

Thus Kraus and Stinespring representations are two views of the same physical structure.

## 14. The Choi representation

Let input dimension be $d$ and define

```math
|\Phi\rangle
=
\frac1{\sqrt d}
\sum_{j=1}^{d}
|j\rangle|j\rangle.
```

Apply the channel to one half:

```math
J(\mathcal E)
=
(\mathcal E\otimes I)
\left(
|\Phi\rangle\langle\Phi|
\right).
```

Up to normalization convention, this is the Choi operator/state associated with the map.

A map is completely positive exactly when its Choi operator is positive semidefinite.

Trace preservation becomes a partial-trace constraint on the Choi operator.

## 15. Why the Choi representation is powerful

The Choi representation turns a map into an operator.

This allows channel questions to be studied using state-like linear algebra:

```text
channel positivity
-> operator positivity

channel tomography
-> state-like reconstruction

channel distance
-> operator optimization
```

It is central in:

- process tomography,
- channel discrimination,
- quantum combs,
- process learning,
- semidefinite programming.

## 16. Composition

Sequential quantum processes compose as

```math
\rho
\xrightarrow{\mathcal E_1}
\mathcal E_1(\rho)
\xrightarrow{\mathcal E_2}
\mathcal E_2(\mathcal E_1(\rho)).
```

The combined channel is

```math
\mathcal E_2\circ\mathcal E_1.
```

A noisy circuit is therefore more accurately modeled as a composition of ideal gates and noise channels than as one global unitary.

## 17. Parallel composition

Independent channels acting on separate systems combine through the tensor product:

```math
\mathcal E_A\otimes\mathcal E_B.
```

If correlations exist in the environment, however, noise may not factorize this way.

This distinction matters for correlated error models and multi-qubit hardware characterization.

## 18. Measurements as channels and instruments

A measurement can be viewed as a quantum-to-classical channel.

For POVM elements $\{E_y\}$,

```math
\mathcal M(\rho)
=
\sum_y
\mathrm{Tr}(E_y\rho)
|y\rangle\langle y|.
```

A quantum instrument keeps both the outcome and the conditional post-measurement state.

Thus measurement is naturally included in the channel formalism.

## 19. Channel distinguishability

Suppose an unknown process is either $\mathcal E$ or $\mathcal F$.

The optimal strategy may use:

- a carefully chosen input state,
- entanglement with a reference,
- an output measurement.

This is why complete positivity and reference systems are operationally important.

The relevant channel distance is often stronger than comparing outputs on one fixed state.

## 20. Fixed points and steady states

A state $\rho_*$ is a fixed point of a channel if

```math
\mathcal E(\rho_*)
=
\rho_*.
```

Repeated channel application can drive systems toward steady states.

This perspective is important in:

- dissipative state preparation,
- quantum reservoir computing,
- open-system QML,
- error-correction dynamics.

## 21. Parameterized quantum channels

A trainable model need not have the form

```math
\rho
\mapsto
U(\theta)\rho U^\dagger(\theta).
```

It can instead be

```math
\rho
\mapsto
\mathcal E_{\boldsymbol\theta}(\rho).
```

The parameters may control:

- unitary interactions,
- environment couplings,
- measurement strengths,
- reset probabilities,
- dissipative rates,
- adaptive branches.

This enlarges the hypothesis class beyond closed-system PQCs.

## 22. Why this matters for QML

Many standard QML models implicitly assume

```text
encode data
-> unitary PQC
-> final measurement.
```

The channel viewpoint allows a broader question:

> Could useful learning architectures be fundamentally open-system, dissipative, measurement-driven, or adaptive?

A model with intermediate measurements and resets is naturally a quantum channel, not one unitary transformation on the visible system.

## 23. Common misconceptions

### “Every physical quantum operation is unitary.”

Only closed deterministic evolution on an isolated system is unitary. General subsystem dynamics are channels.

### “Positive maps are enough.”

No. Local processes must remain positive when acting on part of an entangled system, which motivates complete positivity.

### “A Kraus decomposition uniquely describes microscopic errors.”

No. Kraus representations are generally nonunique.

### “Noise is external to quantum algorithms.”

On real hardware, noise is part of the physical channel implementing the computation and affects complexity and trainability.

## 24. Exercises

### Conceptual

1. Why does entanglement with an untouched reference motivate complete positivity?
2. Explain the physical meaning of Stinespring dilation.
3. Why is a Kraus representation nonunique?
4. Distinguish a channel from a measurement instrument.

### Computational

5. Verify trace preservation for the amplitude-damping Kraus operators.
6. Apply the dephasing channel to

```math
|+\rangle\langle+|
```

and compute the resulting density matrix.
7. Show that amplitude damping is nonunital by computing $\mathcal E(I)$.
8. For a unitary channel $\mathcal U(\rho)=U\rho U^\dagger$, identify a one-operator Kraus representation.

### Research-oriented

9. Design a variational model whose trainable parameters control dissipation rather than only unitary gates.
10. What benchmark would fairly compare a unitary QML model with a parameterized open-system channel model?
11. How could correlated noise invalidate an analysis assuming tensor-product single-qubit channels?
12. Why might learning a quantum process require a richer object than learning input-output state pairs independently?

## 25. Key takeaways

- Quantum channels are the general deterministic state transformations of quantum theory.
- Complete positivity is required because systems may be entangled with external references.
- Kraus, Stinespring, and Choi representations describe the same channel from different perspectives.
- Noise, measurement, reset, and dissipation fit naturally into the channel framework.
- A trainable quantum model can be a parameterized channel rather than a unitary PQC.
- Channel language is essential for process learning, open-system QML, and realistic hardware analysis.

## References

1. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018. https://cs.uwaterloo.ca/~watrous/TQI/
2. K. Kraus, *States, Effects, and Operations*, Springer, 1983.
3. W. F. Stinespring, "Positive Functions on C*-Algebras," *Proceedings of the AMS* 6, 211–216 (1955). https://doi.org/10.1090/S0002-9939-1955-0069403-4
