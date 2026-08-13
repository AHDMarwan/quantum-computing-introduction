# Quantum Resource Theories

## 1. Why resource theories are useful

Quantum information often asks a question more precise than

> Is this state quantum?

A resource theory asks instead:

> Relative to a specified set of free operations, what states or processes enable tasks that free objects cannot perform?

A resource theory therefore formalizes operational scarcity.

Its core ingredients are

```math
\boxed{
\text{free states}
+
\text{free operations}
+
\text{resource monotones}
+
\text{conversion tasks}
}
```

The definition of a resource is always relative to the allowed operations.

## 2. Learning objectives

After this chapter, you should be able to:

- define free states and free operations,
- explain why resources are relative rather than absolute,
- define resource monotones,
- distinguish resource detection from resource quantification,
- formulate state-conversion problems,
- explain entanglement and coherence as resource theories,
- describe magic as a computational resource,
- explain asymmetry and non-Gaussianity at a conceptual level,
- and reformulate vague QML “quantumness” claims as explicit resource questions.

## 3. General structure

Let $\mathcal F$ denote a set of free states and let $\mathfrak F$ denote a set of free operations.

A free operation should preserve freeness:

```math
\rho\in\mathcal F
\Longrightarrow
\mathcal E(\rho)\in\mathcal F
```

for every

```math
\mathcal E\in\mathfrak F.
```

Any state outside $\mathcal F$ is a resource state.

## 4. Why “free” is operational

The word free does not mean physically zero cost.

It means that the theory declares certain states or transformations available without consuming the resource being studied.

For example, in entanglement theory, local quantum operations are allowed even though they may be technologically difficult.

The resource restriction is conceptual:

```text
what can be done
without using the target resource?
```

## 5. Resource monotones

A resource monotone $R(\rho)$ should not increase under deterministic free operations:

```math
R(\mathcal E(\rho))
\le
R(\rho),
\qquad
\mathcal E\in\mathfrak F.
```

Often one also requires:

- $R(\rho)=0$ for free states,
- convexity,
- monotonicity on average under selective operations,
- additivity or subadditivity in appropriate settings.

Different monotones can quantify different operational aspects of the same resource.

## 6. Resource conversion

A central question is whether

```math
\rho
\longrightarrow
\sigma
```

is possible using only free operations.

If not exactly, one can ask about approximate or asymptotic conversion rates.

For many copies,

```math
\rho^{\otimes n}
\longrightarrow
\sigma^{\otimes m},
```

the asymptotic rate

```math
\frac mn
```

can become a fundamental operational quantity.

This is how static resource measures become connected to tasks.

## 7. Entanglement as the prototype

In a standard resource theory of bipartite entanglement:

- free states are separable states,
- free operations include LOCC,
- Bell pairs are canonical resource units.

A valid entanglement monotone should not increase under LOCC.

Examples include entropy of entanglement for pure states and negativity or other mixed-state measures.

This resource theory formalizes why local operations and classical communication cannot create shared entanglement from scratch.

## 8. Coherence as a resource

Choose a preferred reference basis

```math
\{|i\rangle\}.
```

Incoherent states are diagonal:

```math
\rho
=
\sum_i p_i|i\rangle\langle i|.
```

Off-diagonal terms represent coherence relative to that basis.

A common measure is the $l_1$ coherence

```math
C_{l_1}(\rho)
=
\sum_{i\neq j}
|\rho_{ij}|.
```

Another is relative entropy of coherence

```math
C_{\mathrm{rel}}(\rho)
=
S(\Delta(\rho))-S(\rho),
```

where $\Delta$ removes off-diagonal terms in the reference basis.

## 9. Coherence is basis dependent

The state

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}
```

is coherent in the computational $Z$ basis.

But it is an eigenstate in the $X$ basis.

Therefore coherence is not an absolute state property independent of a reference structure.

This is an important conceptual example of resource relativity.

## 10. Dephasing as resource destruction

Define the complete dephasing map

```math
\Delta(\rho)
=
\sum_i
|i\rangle\langle i|
\rho
|i\rangle\langle i|.
```

This removes basis coherence.

For

```math
|+\rangle\langle+|,
```

we obtain

```math
\Delta(|+\rangle\langle+|)
=
\frac I2.
```

The lost off-diagonal terms are precisely the resource used for interference in that basis.

## 11. Magic as a computational resource

Clifford circuits acting on stabilizer states and followed by Pauli measurements admit efficient classical simulation through the stabilizer formalism.

Universal fault-tolerant computation requires additional non-Clifford resources.

States used to inject such operations are called **magic states**.

A resource theory of magic treats stabilizer operations as free and non-stabilizer states/operations as resources.

This gives a sharper computational question than simply asking whether a circuit contains entanglement.

## 12. Stabilizer versus universal computation

Clifford operations include gates such as

```text
H
S
CNOT
```

and map Pauli operators to Pauli operators under conjugation.

Adding a suitable non-Clifford gate such as a $T$ gate enables universality.

From a fault-tolerant perspective, non-Clifford operations can be especially expensive because they may require magic-state distillation.

Thus resource cost can become directly tied to physical hardware overhead.

## 13. Asymmetry

A state can be a resource because it breaks a symmetry.

If allowed operations must commute with a group action, then asymmetric states provide reference-frame information unavailable to symmetric states.

Examples include phase references and clocks.

This connects resource theory to:

- metrology,
- conservation laws,
- quantum thermodynamics,
- time-translation symmetry.

## 14. Thermodynamic resources

In a thermodynamic resource theory, equilibrium Gibbs states may be free and allowed operations preserve appropriate energetic constraints.

A nonequilibrium state then becomes a resource.

Quantities related to free energy can serve as monotones under restricted thermodynamic operations.

The resource framework separates

```text
physical law
from
resource consumption.
```

## 15. Non-Gaussianity

In continuous-variable quantum information, Gaussian states and Gaussian operations have special structure and can often be efficiently characterized.

Non-Gaussian states or operations can serve as resources for tasks that Gaussian processing alone cannot achieve, including universal continuous-variable computation.

Again, the resource depends on the chosen free operational class.

## 16. Contextuality and computational resources

Contextuality has also been studied as a nonclassical resource related to quantum computation in specific models.

The important methodological lesson is that many different forms of nonclassicality exist:

```text
entanglement
coherence
magic
contextuality
asymmetry
non-Gaussianity
```

They should not be conflated.

A quantum speedup might depend on one resource while being insensitive to another.

## 17. Detection versus quantification

A witness can detect the presence of a resource without measuring how much resource is present.

For example, an entanglement witness can satisfy

```math
\mathrm{Tr}(W\sigma)\ge0
```

for all separable states but

```math
\mathrm{Tr}(W\rho)<0
```

for some entangled $\rho$.

This certifies resource presence but does not uniquely quantify its amount.

The same distinction appears in many resource theories.

## 18. Robustness measures

A general resource measure can ask how much free noise must be mixed into a state before it becomes free.

Schematically, define the smallest $s\ge0$ such that

```math
\frac{\rho+s\tau}{1+s}
\in
\mathcal F.
```

The choice of allowed $\tau$ determines a robustness measure.

Robustness quantities often have operational interpretations in discrimination or advantage tasks.

## 19. Resource destroying maps

A resource-destroying map removes the resource while leaving free states unchanged.

For coherence, the dephasing channel is the canonical example:

```math
\Delta(\rho)
```

removes off-diagonal terms.

This suggests a useful experimental methodology:

```text
original model
vs
resource-destroyed model
```

If performance survives resource destruction, that resource was not necessary for the observed effect.

## 20. Resource ablations in QML

This idea is particularly useful for QML.

Suppose a quantum model uses coherent superposition between two computational sectors. Apply a dephasing map that destroys only the cross-sector coherence while preserving populations.

Then compare:

```math
\mathcal M_{\mathrm{coherent}}
```

with

```math
\mathcal M_{\mathrm{dephased}}.
```

If performance differs under equal budgets, the removed coherence becomes a candidate explanatory resource.

This is much stronger than saying merely that the original circuit was “quantum.”

## 21. Necessary versus sufficient resources

Two distinct research questions are:

### Necessity

Does removing resource $R$ destroy the advantage?

### Sufficiency

Does having resource $R$ guarantee an advantage?

A resource can be necessary but not sufficient.

For example, non-Cliffordness may be necessary for universality in a computational model, but an arbitrary non-Clifford circuit need not solve a useful problem faster than classical algorithms.

This distinction is essential in QML.

## 22. Resource thresholds

One can seek threshold theorems of the form

```math
R(\mathcal M)
\le
R_c
\Longrightarrow
\text{efficient classical simulation},
```

while above the threshold some classically hard behavior becomes possible.

Such results can turn qualitative ideas about “quantumness” into quantitative complexity boundaries.

## 23. Resource cost versus resource amount

The amount of a resource in a state is not always the same as the operational cost of generating it.

For example, two states can contain similar entanglement entropy while requiring very different circuit depths under restricted geometries.

Therefore resource accounting may require both:

```text
state resource
and
preparation resource.
```

This matters for practical quantum algorithms and learning models.

## 24. Why resource theories matter for QML

Instead of asking

> Is this QML model quantum enough?

ask:

- Does the model require coherence?
- Is entanglement necessary?
- Does removing magic make it classically simulable?
- Is direct access to noncommuting quantum data the critical resource?
- Is adaptive measurement essential?
- Does the advantage disappear under dephasing?

These questions can support theorem-level claims.

## 25. A resource-theoretic template for learning advantage

A clean research program is:

1. define a task family $\mathcal T$;
2. define free models $\mathcal F$;
3. define a resource $R$;
4. prove a classical/free-model bound;
5. construct a resourceful quantum model beating the bound;
6. quantify the minimal resource required.

Symbolically,

```math
\inf_{\mathcal M\in\mathcal F}
L(\mathcal M)
>
\inf_{\mathcal M:R(\mathcal M)>0}
L(\mathcal M)
```

under matched operational resources.

This is substantially sharper than an empirical QML benchmark alone.

## 26. Common misconceptions

### “Entanglement is the quantum resource.”

There is no single universal quantum resource. The relevant resource depends on the operational restrictions.

### “If a state is nonclassical, it is useful.”

Resource presence does not guarantee usefulness for a particular task.

### “Resource monotones measure computational speedup directly.”

Not generally. A monotone quantifies a resource under a chosen theory; connecting it to speedup requires an additional theorem.

### “More resource always means better performance.”

No. Excess resource can be irrelevant or even harm trainability.

## 27. Exercises

### Conceptual

1. Why is a resource defined relative to free operations rather than absolutely?
2. Explain why $|+\rangle$ is coherent in one basis but not another.
3. Why does magic provide a different notion of computational resource from entanglement?
4. Distinguish resource necessity from resource sufficiency.

### Computational

5. Compute the $l_1$ coherence of

```math
|+\rangle\langle+|.
```
6. Apply complete dephasing to a general qubit density matrix

```math
\rho
=
\begin{pmatrix}
a&c\\
c^*&1-a
\end{pmatrix}.
```
7. Verify that dephasing leaves every incoherent state unchanged.
8. For a proposed monotone $R$, explain what inequality it must satisfy under free operations.

### Research-oriented

9. Choose one QML architecture and propose a resource-destroying ablation that tests whether entanglement, coherence, or another resource is necessary.
10. Formulate a dequantization boundary theorem using a resource threshold.
11. How would you distinguish “high resource amount” from “high resource preparation cost” experimentally?
12. What resource theory might be appropriate for learning directly from noncommuting quantum experiments?

## 28. Key takeaways

- A quantum resource is defined relative to a set of free operations.
- Resource theories separate free states, free transformations, monotones, and conversion tasks.
- Entanglement, coherence, magic, asymmetry, contextuality, and non-Gaussianity are distinct resources.
- Resource presence does not automatically imply task advantage.
- Resource-destroying maps provide powerful causal ablations for quantum algorithms and QML.
- Resource-theoretic formulations can sharpen vague quantum-advantage claims into necessity, sufficiency, and threshold questions.

## References

1. E. Chitambar and G. Gour, "Quantum resource theories," *Reviews of Modern Physics* 91, 025001 (2019). https://doi.org/10.1103/RevModPhys.91.025001
2. T. Baumgratz, M. Cramer, and M. B. Plenio, "Quantifying Coherence," *Physical Review Letters* 113, 140401 (2014). https://doi.org/10.1103/PhysRevLett.113.140401
3. V. Veitch et al., "The resource theory of stabilizer quantum computation," *New Journal of Physics* 16, 013009 (2014). https://doi.org/10.1088/1367-2630/16/1/013009
